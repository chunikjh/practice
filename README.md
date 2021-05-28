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
 
