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

-   string, Arrays, struct

### 3. mapping type

## gas 와 ether 의 단위.

-   gas는 smart contract 를 사용하기 위한 비용(단위) // 개발자는 해당 값을 줄이기 위해서 고민이 필요한 부분.

## Function_1.

### function 기본 사용 틀

>

    function 이름 () public { // (public, private, interval, external) 변경가능.
        내용
    }

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

## Funtion_2 / 접근 제어자(Visibility Modifiers)

1. public: 모든 곳에서 접근 가능
2. external: public 처럼 모든 곳에서 접근 가능하나, external이 정의된 자기자신 컨트랙 내에서 접근 불가
3. private: 오직 private이 정의된 자기 컨트랙에서만 가능(private이 정의된 컨트랙을 상속 받은 자식도 불가능)
4. internal: private처럼 오직 internal 이 정의된 자기 컨트랙에서만 가능하고, internal 이 정의된 컨트랙을 상속  
   (internal contract <- internal contract child contract)

>

    # contract1
    contract Public_example {
        uint256 public a = 3;

        function changeA(uint256 _value) external  {
            a =_value;
        }
        function get_a() view external returns (uint256){
            return a;
        }
    }

    # contract2
    contract Public_example_2 {
        Public_example instance = new Public_example();

        function changeA_2(uint256 _value) public {
            instance.changeA(_value);
        }
        function use_public_example_a() view public returns (uint256){
            return instance.get_a();
        }
    }

## Function_3 / View 와 Pure

1. view: function 밖의 변수들을 읽을 수 있으나 변경 불가능.
2. pure: function 밖ㅇ의 변수들을 읽지 못하고 변경도 불가능.
3. view 와 pure 둘다 명시 안할 떄: funtion 밖의 변수들을 읽어서, 변경을 해야할 떄 사용.

>

    uint256 public a =1;

    function read_a() public view returns (uint256){
    return a+2;
    }

    // 2. pure
    function read_a2() public pure returns (uint256){
    uint256 b=1;
    return 4+2+b;
    }

    // 3. viwe, pure 둘다 사용 x
    function read_a3() public returns (uint256){
    a = 13;
    return a;
    }

## Function_4 / 4개의 저장영역과 String

1. storage: 대부분의 변수, 함수들이 저장되며, 영속적으로 저장이 되어 가스 비용이 비싸다는 특징이 있습니다.
2. memory: 함수의 파라미터, 리턴값, 레퍼런스 타입이 주로 저장이 됩니다.  
   그러나, storage 처럼 영속적이지 않고 함수내에서만 유효하기에 storage보다 가스 비용이 싸다는 특징이 있습니다.
3. Colldata: 주로 external function의 파라미터에서 사용 됩니다.
4. stack: EVM (Ethereum Virtual Machine) 에서 stack data를 관리할 때 쓰는 영역이며, 1024Mb 제한적입니다.

## instance_1
