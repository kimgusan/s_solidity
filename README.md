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

-   하나의 contract 에서 다른 contract 을 연결할 때 사용.

## instance - constructor(생성자)\_2

-   변수의 값을 초기화 할 때 사용.
-   인스턴스화 할 때 gas 의 소비 상태를 중요시 해야함.

#### A 를 쓰기 위해서는 constructor를 지정해줘야 한다는 내용.

    // contractA 에 위치
    constructor(string memory _name, uint256 _age){
        name = _name;
        age = _age;
    }

    // contractB 에 위치
    A instance = new A("Alice", 52);

## 상속\_1

    contract Father{
        string public familyName = "Kim";
        string public givenName = "Jung";
        uint256 public money = 100;

            constructor(string memory _givenName) {
                giverName = _givenName;
            }

            function getFamilyName() view public returns(string memory){
                return familyName;
            }

            function getGivenName() view public returns(string memory){
                return givenName;
            }

            function getMoney() view public returns(uint256){
                return money;
            }

    }

    // // 상속을 원하는 contract 를 is "명칭" 을 써준다. (기본)
    // contract Son is Father{
    // }

    // constructor 사용
    contract Son is Father("James"){

    }

## 상속\_overriding_2

#### virtual

    function getMoney() view public virtual returns(uint256){
        return money;
    }

---

#### override

    function getMoney() view override public returns(uint256){
        return money + earning;
    }

## 상속\_N개이상\_3

-   override 기능을 사용하여 표현해줘야 함. (부모 contract 에는 겹치는 함수에 대해서 virtual 을 명시해줘야 하며, 자식 함수에는 override를 이용하여 상속받을 contract 에 대하여 작성해줘야 한다.)

>

    contract Son is Father, Mother{
        function getMoney() public view override(Father, Mother) returns(uint256){
            return fatherMoney + motherMoney;
        }

}

## event_1

-   print 구문이 없고 **block 내부에 저장하는 과정을 event** 라고 한다.
    (단순하게 block event 라는 명칭으로 저장한다고 생각하면 된다.)

        contract lec13{

            event info(string name, uint256 money);

            // 예시로 만드는 함수
            function sendMoney() public {
                emit info("KimDaeJin", 1000);
            }
        }

## evnet_indexed_2

-   이벤트에 적용되는 인덱스.
-   evnet 항목에서 원하는 값만 가져오기 위해서는 **indexed** 를 정의해줘야 합니다.

        contract lec14{

        event numberTracker(uint256 num, string str);
        event numberTracker2(uint256 indexed num, string str);

        uint256 num = 0;
        function PushEvent(string memory _str) public {
            emit numberTracker(num, _str);
            emit numberTracker2(num, _str);
            num++;
        }

    }

## 상속\_super_4

-   상속받는 부모의 함수의 내용이 길 때 해당 함수 자체를 가져오는 키워드.

>

    contract Father {
        event FatherName(string name);

        function who() public virtual{
        emit FatherName("KimDaeho");
        }

    }

    contract Son is Father{
        event sonName(string name);

    function who() public override {
        super.who(); // 상속받는 부모의 함수의 내용이 길 때 해당 함수 자체를 가져오는 키워드.
        emit sonName("Kimjin");
        }

    }

## 상속\_순서\_5

-   상속 받은 항목의 가장 마지막에 작성된 (오른쪽 최신 항목)의 함수를 가져옵니다.

#### Mother의 function who() 함수를 상속받는다.

>

    contract Son is Father, Mother{
        function who() public override (Father, Mother){
        super.who();
        }
    }

#### Father의 function who() 함수를 상속받는다.

>

    contract Son is Mother, Father{
        function who() public override (Father, Mother){
        super.who();
        }
    }

## Mapping

-   **key, value** 로 구성.
-   mapping 에는 length 기능이 없다.

>

    contract lec17{

        // key 값의 형식 => value의 형식 (mapping의 이름도 정의 해줘야 한다. : ageList);
        mapping (uint256=>uint256) private ageList;
        mapping (string=>uint256) private priceList; // key: 아이템 , value: 가격
        mapping (uint256=>string) private nameList; // key: 가격 , value: 아이템

        function setAgeList(uint256 _index, uint256 _age) public {
            // key 값과 value 값을 넣어주는 함수.
            ageList[_index] = _age;
        }

        function getAge(uint256 _index) public view returns(uint256){
            // 특정 key 값의 value 값을 가져오는 함수.
            return ageList[_index];
        }

        function setPriceList(string memory _itemName, uint256 _price) public {
            priceList[_itemName] = _price;
        }

        function getPrice(string memory _index) public view returns(uint256){
            return priceList[_index];
        }

        function setNameList(uint256 _index, string memory _name) public {
            nameList[_index] = _name;
        }

        function getName(uint256 _index) public view returns(string memory){
            return nameList[_index];
        }

## Array(배열)
- python array와는 다른 어떠한 부분을 가지고 있으며, 스마트 컨트렉에 대하여 우선적으로 학습 예정