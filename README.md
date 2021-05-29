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
