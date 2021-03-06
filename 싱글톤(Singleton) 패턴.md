# 싱글톤(Singleton) 패턴

어플리케이션이 실행될 때 어떤 클래스가 **최초 한번만 메모리를 할당하고(static)** 그 메모리에 인스턴스를 만들어 사용하는 디자인 패턴

- 객체의 인스턴스가 오직 1개만 생성
  - 하나의 인스턴스를 메모리에 등록해서 여러 쓰레드가 동시에 해당 인스턴스를 공유하여 사용할 수 있게끔하여 요청이 많은 곳에서 사용하면 효율 높이기가 가능하다.
- 생성자가 여러 차례 호출되어도 실제로 생성하는 객체는 하나고 최초 생성 이후에 호출된 생성자는 최초에 생성한 객체를 반환한다
  - Java에선 생성자 : private으로 선언하여 생성 불가하게 하고 getinstance()로 받아쓰기도 한다.

<aside> 📌 싱글톤 패턴은 동시성(Concurrency) 문제를 고려해서 설계해야 한다.</aside>

동시성 : 여러 요청이 동시에 동일한 자원에 접근하고 수정하려는 것

### 싱글톤 패턴 사용 이유

1. 고정된 메모리 영역을 얻으면서 **한번의 new**로 인스턴스를 사용하기 때문에 메모리 낭비를 방지할 수 있다.
2. 싱글톤으로 만들어진 **클래스의 인스턴스는 전역**이기 때문에 다른 클래스의 인스턴스들이 데이터를 공유하기 쉽다.
3. 인스턴스가 **절대적으로 한 개만 존재하는 것**을 보증하고 싶을 경우 사용
4. 두 번째 이용시 부터는 객체 로딩 시간이 줄어 성능이 좋아진다.

<aside> 📌 싱글톤 패턴은 DBCP(DataBaseCommection Pool)처럼 공통된 객체를 여러개 생성해야 하는 상황에서 많이 사용

</aside>

### 싱글톤 패턴의 무분별한 사용을 지양

싱글톤 인스턴스가 많은 일이나 데이터를 공유시킬 경우 다른 클래스의 인스턴스들간에 결합도가 높아진다.

→ 객체 지향 설계 원칙에 어긋나는 **개방-폐쇄 원칙** 위배

- 수정이 어려워 지고 유지보수의 비용이 높아진다.
- 멀티쓰레드 환경에서 동기화 처리를 안하면 인스턴스가 2개가 생성될 수 있는 가능성이 생기게 된다.

**개방-폐쇄 원칙이란?**

객체를 다룸에 있어 객체의 확장은 개방적으로, 객체의 수정은 폐쇄적으로 대하는 원칙

- ex) 기능이 변하거나 확장 가능, 해당 기능의 코드는 수정이 안된다.
  - 객체를 하나 수정함으로써 해당 객체에 의존하는 다른 객체들의 코드까지 다 고쳐야 한다면 좋은 설계가 아니다.
- **객체 간의 의존성을 최소화하여 코드 변경에 따른 영향력을 낮추기  위한 원칙**

```java
public class CarClass {

    // 객체의 인스턴스가 하나만 존재하도록 하려면?
    
    // 자신을 멤버로 선언해서 메모리에 올려놓는다(static)
    // 멤버로 선언된 CarClass도 private
    private static CarClass car = new CarClass();

    // 생성자가 private라서 객체 생성 불가능
    private CarClass() {}

    //외부에서 멤버로 선언된 car를 가져올 수 있는 method를 만들면 된다.
    public static CarClass getInstance(){
        return car;
    }

    // getInstance메소드 외에는 CarClass객체를 생성 및 사용이 불가능
}
```

private static CarClass car = new CarClass(); 를 통해 최초 한번만 객체를 생성하고 이후에 해당 객체를 getInstance 메소드를 활용해 return 받아 사용하는데 해당 차 객체를 이용이 불가능 하게끔 구현했다.

→ 싱글톤 패턴을 활용한 방식