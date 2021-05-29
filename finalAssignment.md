/*
MySQL로 테이블 제작하기 
CREATE TABLE `study`.`settlement` (
`idsettlement` BIGINT NOT NULL AUTO_INCREMENT,
`user_id` BIGINT NOT NULL,
`price` DECIMAL(12,4) NULL,
PRIMARY KEY (`idsettlement`));
*/

[UserApiController.java]에 아래 내용 추가
@GetMapping("/settlement/{id}")
public Header orderPrice(@PathVariable Long Id){
      return userApiLogicService.orderPrice(id);
}

[UserApiLogicService.java]에 아래 내용 추가
@Autowired
private OrderGroupRepository orderGroupRepository;

@Autowired
private UserRepository userRepository;

public Header orderPrice(Long Id){

     return Optional.ofNulllable(orderGroupRepository.findById(id))
             .map(body ->{
                 OrderGroup orderGroup = OrderGroup.builder()
	                .userId(userRepository.getOne(body.getUserId()))
			.totalPrice(body.getTotlaPrice())
			.build();
		return orderGroup;
	    })
	    .orElseGet(() -> Header.ERROR("구매 이력 없음"));
}
