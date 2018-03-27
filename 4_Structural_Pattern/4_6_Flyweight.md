플라이급 패턴(Flyweight pattern)
* 최종 정리
- 같은 객체를 여러번 만들지 않고 관리하는 매니저를 만들어서 매니저가 이미 생성된 객체면 그걸 주고 없으면 만들어 주는 패턴 
    ->즉, Flyweight pool을 만들고 거기에 싹다 모아 놓고 필요하면 참조해서 사용 하는 방식
- 객체로 만들기에는 너무 작은 규모를 관리 할때 필요 하다 (문서 편집기에서 글자 하나하나 같은 경우)

* Inflearn
- 플라이이웨이트 패턴을 통해 '메모리 공간'을 절약할 수 있다
- 예제 시나리오
    -> 클라이언트가 같은 이미지를 여러번 사용할 때 매번 객체를 만드는 메모리 비효율을 해소
    -> Img Manager를 만들어서 이미지를 관리 하게 한다
- ex
```java
public class Main {
    public static vodi main(String[] args){
        FlyweightFactory factory = new FlyweightFactory();
        Flyweight flyweight = facotry.getFlyweight("a");
    }
}
public class Flyweight {
    private String data;

    public Flyweight(String data){
        this.data = data;
    }
}
public class FlyweightFactory { // Flyweight Manager class
    Map<String, Flyweight> pool;

    public FlyweightFactory(){
        pool = new TreeMap<>();
    }
    public getFlyweight(String key){
        Flyweight flyweight = pool.get(key);
        if(flyweight ==null){}
            new Flyweight(key);
            pool.put(key, flyweight);
        }else{
            print("재사용")
        }
        return flyweight;
    }
}
```
* GOF
1. 의도 : 공유(sharing)을 통해 많은 수의 소립(fine-grained) 객체들을 효과적으로 지원한다

2. 동기 
- 설계의 하단을 실제로 구현하는 비용이 만만치 않은 응용프로그램들이 있다 
- 플라이급 객체는 공유 가능한 객체로, 여러 비슷한 상황에서 사용될 수 있고, 각각의 상황에서는 독립적인 객체로 동작한다
    -> 공유될 수 없는 객체의 인스턴스와 구분이 안 된다는 의미
    -> 따라서 플라이급 객체가 적용될 상황을 미리 가정하면서 개발할 수는 없다
- 프라리이급 패턴에서 중요한 개념은 '본질적'상태와 '부가적'상태의 구분이다
    -> 본질적 상태는 플라이급 객체에 저자오디어야 하며, 이것이 적용되는 상황과 상관없는 본질적 특성정보들이 객체를 구성한다
    -> 부가적 상태는 플라이급 객체가 사용될 상황에 따라 달라질 수 있고, 그 상황에 종속적이다 -> 공유될 수 없다

3. 활용성
- 응용프로그램이 대량의 객체를 사용 해야 할 때
- 객체의 수가 너무 많아져 저장 비용이 너무 높아 질 때
- 대부분의 객체 상태를 부가적인 것으로 만들 수 있을 때
- 부가적인 속성들을 제거한 후 객체들을 조사해 보니 객체의 많은 묶음이 비교적 적은 수의 공유된 객체로 대체될 수 있을 때.
  현재 서로 다른 객체로 간주한 이유는 이들 부가적인 속성 때문이었지 본질이 달랐던 것은 아닐 때
- 응용프로그램이 객체의 정체성에 의존하지 않을 때. 플라이급 객체들은 공유 될 수 있음을 의미하는데, 식별자가 있다는 것은 서로 다른
  객체로 구별해야 한다는 의미이므로 플라이급 객체를 사용 할 수 없다