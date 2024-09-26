# Solidity (솔리디티).

: 이더리움, 클레이튼에서 지원하는 스마트 컨트랙트 언어.

-   Smart contracts: 미리 정의된 조건이 충족되면 블록체인 안의 저장된 프로그램이 실행되는 것.

\*\* remix: react 기반의 IDE

## Solidity Type.

: 3가지 타입으로 나눌 수 있습니다.

### 1. data type

-   **boolean**: `true` / `false` 값을 가집니다.
-   **bytes**: 고정 크기의 바이트 배열 (1 ~ 32) 또는 동적 크기 바이트 배열입니다.
-   **address**: 이더리움 주소를 저장합니다.
-   **int / uint**: 부호가 있는 정수(`int`)와 부호가 없는 정수(`uint`)로 나뉩니다.

>

    boolean: true / false

    bool public b = false;

    // ! // == && (다른 연산자가 존재한다)
    bool public b1 = !false; // true
    bool public b2 = false || true; // true
    bool public b3 = false == true; // false
    bool public b4 = false && true; // false


    // bytes 1 ~ 32
    bytes4 public bt = 0x12345678;
    bytes public bt2 = "STRING";

    // address :
    address public addr = 0x7EF2e0048f5bAeDe046f6BF797943daF4ED8CB47;

    // int vs uint: (음수가 존재하는지 아닌지에 따른 구분이 이뤄진다)
    // int: -2^7 ~ 2^7 -1
    // uint: 0 ~ 2^7 -1
    int8 public it =4;

    // uint8:
    // 0 ~ 2^8 -1
    // uint == uint256
    uint256 public uit = 132213;
    // + - * / : 사칙연산 사용 가능

    // 범위를 넘겼기 때문에 에러 발생
    // uint8 public uit2 = 256;

### 2. reference type

### 3. mapping type

## gas 와 ether 의 단위.

-   gas는 smart contract 를 사용하기 위한 비용(단위) // 개발자는 해당 값을 줄이기 위해서 고민이 필요한 부분.

## Function.

> function 기봉 사용 틀

> function 이름 () public { // (public, private, interval, external) 변경가능.

        // 내용

### 총 3개의 방식이 존재

1. Parameter 와 Return 값이 없는 function 정의.
2. Parameter는 있고 Return 값이 없는 function 정의.
3. Parameter와 Return 값이 있는 function 정의.

>

    // 1. Parameter 와 Return 값이 없는 function 정의.
    uint256 public a = 3;

    function changeA1 () public{
        a = 5;
    }

>

    // 2. Parameter는 있고 Return 값이 없는 function 정의.
    function changeA2 (uint256 _value) public{
        a = _value;
    }

>

    // 3. Parameter와 Return 값이 있는 function 정의.
    function changeA3 (uint256 _value) public returns(uint256){
        a = _value;
        return a;
    }
