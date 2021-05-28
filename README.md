Using id -> Return user

8-1-04 User API Update

 t UserApiController.java

 @Override
     @DeleteMapping("{id}")      // /api/user/{id}
         public Header delete(@PathVariable Long id) {
	         return userApiLogicService.delete(id);
		     }

		     At UserApiLogicService.java
		     @Override
		         public Header delete(Long id) {
			         // 1. id -> repository -> user
				         Optional<User> optional = userRepository.findById(id);

					         // 2. repository -> delete
						         return optional.map(user -> {
							                 userRepository.delete(user);
									                 return Header.OK();
											                 })
													                .orElseGet(() -> Header.ERROR("데이터없음"));
															    }

