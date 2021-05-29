package com.example.study.controller.api;

import com.example.study.ifs.CrudInterface;
import com.example.study.model.network.Header;
import com.example.study.model.network.request.OrderGroupApiRequest;
import com.example.study.model.network.response.OrderGroupApiResponse;
import com.example.study.service.OrderGroupApiLogicService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping(/api/orderGroup)
public class OrderGroupApiContoller implements CrudInterface<OrderGroupApiRequest, OrderGroupApiResponse> {

    @Autowired
    private OrderGroupApiLogicService orderGroupApiLogicService;

    @Override
    @PostMapping()
    public Header<OrderGroupApiResponse> create(@RequestBody Header<OrderGroupApiRequest> request) {
        return orderGroupApiLogicService.create(request);
    }

    @Override
    @GetMapping({id})
    public Header<OrderGroupApiResponse> read(@PathVariable Long id) {
        return orderGroupApiLogicService.read(id);
    }

    @Override
    @PutMapping()
    public Header<OrderGroupApiResponse> update(@RequestBody Header<OrderGroupApiRequest> request) {
        return orderGroupApiLogicService.update(request);
    }

    @Override
    @DeleteMapping({id})
    public Header delete(@PathVariable Long id) {
        return orderGroupApiLogicService.delete(id);
    }
}

package com.example.study.service;

import com.example.study.ifs.CrudInterface;
import com.example.study.model.entity.OrderGroup;
import com.example.study.model.network.Header;
import com.example.study.model.network.request.OrderGroupApiRequest;
import com.example.study.model.network.response.OrderGroupApiResponse;
import com.example.study.repository.OrderGroupRepository;
import com.example.study.repository.UserRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.time.LocalDateTime;

@Service
public class OrderGroupApiLogicService implements CrudInterface<OrderGroupApiRequest, OrderGroupApiResponse> {

    @Autowired
        private OrderGroupRepository orderGroupRepository;

	    @Autowired
	        private UserRepository userRepository;

		    @Override
		        public Header<OrderGroupApiResponse> create(Header<OrderGroupApiRequest> request) {
			        OrderGroupApiRequest body = request.getData();

				        OrderGroup orderGroup = OrderGroup.builder()
					                .status(body.getStatus())
							                .orderType(body.getOrderType())
									                .revAddress(body.getRevAddress())
											                .revName(body.getRevName())
													                .paymentType(body.getPaymentType())
															                .totalPrice(body.getTotalPrice())
																	                .totalQuantity(body.getTotalQuantity())
																			                .orderAt(LocalDateTime.now())
																					                .user(userRepository.getOne(body.getId()))
																							                .build();

																									        OrderGroup newOrderGroup = orderGroupRepository.save(orderGroup);

																										        return response(newOrderGroup);
																											    }

																											        @Override
																												    public Header<OrderGroupApiResponse> read(Long id) {
																												            return orderGroupRepository.findById(id)
																													                    .map(this::response)
																															                    .orElseGet(()->Header.ERROR("데이터 없음"));
																																	        }

																																		    @Override
																																		        public Header<OrderGroupApiResponse> update(Header<OrderGroupApiRequest> request) {
																																			        OrderGroupApiRequest body = request.getData();

																																				        return orderGroupRepository.findById(body.getId())
																																					                .map(orderGroup -> {
																																							                    orderGroup
																																									                                .setStatus(body.getStatus())
																																													                            .setOrderType(body.getOrderType())
																																																                                .setRevAddress(body.getRevAddress())
																																																				                            .setRevName(body.getRevName())
																																																							                                .setPaymentType(body.getPaymentType())
																																																											                            .setTotalPrice(body.getTotalPrice())
																																																														                                .setTotalQuantity(body.getTotalQuantity())
																																																																		                            .setOrderAt(LocalDateTime.now())
																																																																					                                .setUser(userRepository.getOne(body.getId()));
																																																																									                    return orderGroup;
																																																																											                    })
																																																																													                    .map(orderGroupRepository::save)
																																																																															                    .map(this::response)
																																																																																	                    .orElseGet(()->Header.ERROR("데이터 없음"));
																																																																																			        }

																																																																																				    @Override
																																																																																				        public Header delete(Long id) {

																																																																																					        orderGroupRepository.findById(id)
																																																																																						                .map()
																																																																																								                .orElseGet(()->Header.ERROR("데이터 없음"));
																																																																																										        return null;
																																																																																											    }

																																																																																											        private Header<OrderGroupApiResponse> response(OrderGroup orderGroup){

																																																																																												        OrderGroupApiResponse body = OrderGroupApiResponse.builder()
																																																																																													                .id(orderGroup.getId())
																																																																																															                .status(orderGroup.getStatus())
																																																																																																	                .orderType(orderGroup.getOrderType())
																																																																																																			                .revAddress(orderGroup.getRevAddress())
																																																																																																					                .revName(orderGroup.getRevName())
																																																																																																							                .paymentType(orderGroup.getPaymentType())
																																																																																																									                .totalPrice(orderGroup.getTotalPrice())
																																																																																																											                .totalQuantity(orderGroup.getTotalQuantity())
																																																																																																													                .orderAt(orderGroup.getOrderAt())
																																																																																																															                .arrivalDate(orderGroup.getArrivalDate())
																																																																																																																	                .userId(orderGroup.getUser().getId())
																																																																																																																			                .build();

																																																																																																																					        return Header.OK(body);
																																																																																																																						    }
																																																																																																																						    }

