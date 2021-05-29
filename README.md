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

