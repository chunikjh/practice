package com.example.study.model.network.request 아래에 
ItemApiRequest 자바 파일 생성

package com.example.study.model.network.response 아래에
ItemApiResponse 자바 파일 생성

com.example.study.controller.api 아래에
ItemApiController 자바 파일 생성 CrudInterface 구현

com.example.study.service 아래에
ItemApiLogicService 자바 파일 생성 CrudInterface 구현

ItemApiController 자바파일에서 create() 에 ItemApiLogicService 연동하여 구현

ItemApiController 자바파일에서 read() 에 ItemApiLogicService 연동하여 구현

ItemApiController 자바파일에서 update() 에 ItemApiLogicService 연동하여 구현

ItemApiController 자바파일에서 delete() 에 ItemApiLogicService 연동하여 구현

package com.example.study.model.network.request;

import lombok.AllArgsConstructor;
import lombok.Builder;
import lombok.Data;
import lombok.NoArgsConstructor;

import java.math.BigDecimal;
import java.time.LocalDateTime;

@Data
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class OrderGroupApiRequest{
   private Long id;
   private String status;
   private String orderType;
   private String revAddress;
   private String revName;
   private String paymentType;
   private BigDecimal totalPrice;
   private Integer totalQuantity;
   private LocalDateTime orderAt;
   private LocalDateTime arrivalDate;
   private Long userId;
 }

 copy OrderGroupApiRequest to OrderGroupApiResponse

package com.example.study.controller.api;

import com.example.study.ifs.CrudInterface;
import com.example.study.model.network.Header;
import com.example.study.model.network.request.OrderGroupApiRequest;
import com.example.study.model.network.response.OrderGroupApiResponse;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/api/orderGroup")
public class OrderGroupApiContoller implements CrudInterface<OrderGroupApiRequest, OrderGroupApiResponse> {

    @Override
        @PostMapping("")
	    public Header<OrderGroupApiResponse> create(@RequestBody Header<OrderGroupApiRequest> request) {
	            return null;
		        }

			    @Override
			        @GetMapping("{id}")
				    public Header<OrderGroupApiResponse> read(@PathVariable Long id) {
				            return null;
					        }

						    @Override
						        @PutMapping("")
							    public Header<OrderGroupApiResponse> update(@RequestBody Header<OrderGroupApiRequest> request) {
							            return null;
								        }

									    @Override
									        @DeleteMapping("{id}")
										    public Header delete(@PathVariable Long id) {
										            return null;
											        }
												}
												package com.example.study.service;

												import com.example.study.ifs.CrudInterface;
												import com.example.study.model.network.Header;
												import com.example.study.model.network.request.OrderGroupApiRequest;
												import com.example.study.model.network.response.OrderGroupApiResponse;
												import com.example.study.repository.OrderGroupRepository;
												import com.example.study.repository.UserRepository;
												import org.springframework.beans.factory.annotation.Autowired;
												import org.springframework.stereotype.Service;

												@Service
												public class OrderGroupApiLogicService implements CrudInterface<OrderGroupApiRequest, OrderGroupApiResponse> {

												    @Autowired
												        private OrderGroupRepository orderGroupRepository;

													    @Autowired
													        private UserRepository userRepository;

														    @Override
														        public Header<OrderGroupApiResponse> create(Header<OrderGroupApiRequest> request) {
															        return null;
																    }

																        @Override
																	    public Header<OrderGroupApiResponse> read(Long id) {
																	            return null;
																		        }

																			    @Override
																			        public Header<OrderGroupApiResponse> update(Header<OrderGroupApiRequest> request) {
																				        return null;
																					    }

																					        @Override
																						    public Header delete(Long id) {
																						            return null;
																							        }
																								}

