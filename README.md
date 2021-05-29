[Make Enum]

package com.example.study.model.enumClass;

import lombok.AllArgsConstructor;
import lombok.Getter;

@Getter
@AllArgsConstructor
public enum UserStatus {

    REGISTERED(0,등록,사용자 등록상태),
    UNREGISTERED(1,해지,사용자 해지상태);

    private Integer id;
    private String title;
    private String description;
}

[User],[UserApiRequest],[UserApiResponse] 변경

Enum 생성 -> entity 적용 -> request/response 적용 -> service 변경
단, Enum 설정은 초기에 할것

추상 컨트롤러 생성 -> 컨트롤러 내부 변경(구현 -> 상속) ->PostConstruct 설정

CrudInterface를 구현하는 CrudContoller 추상 클래스에서 baseService 라는 추상 클래스를 받아오면 된다.
Service의 활용을 보면 각각 필요한 repository가 필요하고, 각 repository는 JpaRepository로부터 상속을 받으므로 Entity를 Autowired 해주면 된다. 
BaseService에서 추상화 하는 내용은 Crud의 4개의 method 이므로 CrudInterface를 구현하도록 해야하지만,  LogicService에서 어차피 Override 해야하므로 재정의 할 필요가 없다.

각 Service는 BaseService를 상속을 받으므로, BaseService에는 req, res, entity를 넘겨준다.
BaseService는 CrudInterface를 구현하기 위해서 가지고 있는 제네릭 중에서 req, res를 넘겨주고, JpaRepository를 Autowired로 받기위해서 Entity를 받은 형태이다.
받은 Entity에 따라 미리 작성된 JpaRepository를 상속받은 적절한 Repository가 Component로 사용된다.

각 Controller는 CrudController를 상속받으므로, CrudController에는 해당 req, res, entity를 넘겨준다. 
CrudController는 CrudInterface를 구현하기 위해서 가지고 있는 제네릭 중에서 req, res를 넘겨주고, 4가지 기본 메서드를 재정의한다. 
또한 CrudController는 가지고 있는 제네릭은 BaseService에 넘겨주고, BaseService에서는 받아온 Entity를 이용하여 JpaRepository를 Autowired로 연결시킨다.

BaseService에 걸려있는 req, res, Entity는 각 LogicService가 생성이 될때 상속받으면서 넘겨받은 것이며, 이 값을 이용해서 LogicService에 재정의된 4가지 기본 메서드를 사용한다.

적용하기

package com.example.study.service;

import com.example.study.model.entity.Item;
import com.example.study.model.entity.Partner;
import com.example.study.model.network.Header;
import com.example.study.model.network.request.PartnerApiRequest;
import com.example.study.model.network.response.ItemApiResponse;
import com.example.study.model.network.response.PartnerApiResponse;
import org.springframework.stereotype.Service;

@Service
public class PartnerApiLogicService extends BaseService<PartnerApiRequest, PartnerApiResponse, Partner>{
    @Override
        public Header<PartnerApiResponse> create(Header<PartnerApiRequest> request) {
	        return null;
		    }

		        @Override
			    public Header<PartnerApiResponse> read(Long id) {
			            return baseRepository.findById(id)
				                    .map(this::response)
						                    .orElseGet(()->Header.ERROR("데이터 없음"));
								        }

									    @Override
									        public Header<PartnerApiResponse> update(Header<PartnerApiRequest> request) {
										        return null;
											    }

											        @Override
												    public Header delete(Long id) {
												            return null;
													        }

														    private Header<PartnerApiResponse> response(Partner partner){
														            ItemApiResponse body = ItemApiResponse.builder()
															                    .id(partner.getId())
																	                    .name(partner.getName())
																			                    .status(partner.getStatus())
																					                    .address(partner.getAddress())
																							                    .callCenter(partner.getCallCenter())
																									                    .partnerNumber(partner.getPartnerNumber())
																											                    .businessNumber(partner.getBusinessNumber())
																													                    .ceoName(partner.getCeoName())
																															                    .registeredAt(partner.getRegisteredAt())
																																	                    .unregisteredAt(partner.getUnregisteredAt())
																																			                    .categoryId(partner.getCategory().getId())
																																					                    .build();

																																							            return Header.OK(body);
																																								        }
																																									}
																																							샘플 데이터를 생성하는 방법
																																							1. 코드 파일을 이용하여 직접 생성
																																							2. 이미 작성된 SQL 파일을 import 하기

모든 컨트롤러에 대해서 Header<List<*Response>>를 반환하는 seach() 메서드를 만든다.
Pagination 자바 파일을 생성하여 전체페이지, 전체요소, 현재페이지, 현재요소를 선언하고 seach() 메서드내에서 이것을 이용하여 표시를 위한 최소한의 정보를 제공한다.

//todo Service에서 사용가능하도록 모든 Controller에 적용되도록 추상 클래스로 작성한다.

