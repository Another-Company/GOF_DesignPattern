중재자 (Mediator Pattern)
* 최종 정리
- Me

* Inflearn
- '복잡한 관계'를 간단한 관계로 구현한다
- M:N의 관계를 1:1 관계로 만든다



```java
public abstract class Colleague {
    private Mediator mediator;
    public boolean join(Mediator mediator){
        this.mediator = mediator;
        Mediator.addColleague(this);
    }
    public void sendData(String data){
        if(mediator != null){
            mediator.mediate(data);
        }
    }
    abstract public void handle(String data){
        
    }
}
public abstract class Mediator {
    private List<Colleague> colleagues;
    public boolean addColleague(Colleague colleague){
        if(colleagues != null){
            return colleagues.add(colleague);
        }
        return false;
    }
    public abstract void mediate(String data);
}

public class ChatMediator implements Mediator{
    @Override
    public void mediate(String data){
        for(Colleague colleague : colleagues){
            // 중재 가능성이 있는 정보
            colleague.handle(data);
        }
    }
}
public class ChatColleague implements Colleage {
    @Override
    public void handle(String data){
        println(this + data);
    }
}

public class Main {
    public void main(String[] args){
        Colleague colleague1 = new ChatCollague();
        Colleague colleague2 = new ChatCollague();
        Colleague colleague3 = new ChatCollague();

        Mediator mediator = new ChatMediator();

        colleague1.join(mediator);
        colleague2.join(mediator);
        colleague3.join(mediator);

        colleague1.sendData("AAA");
        colleague2.sendData("AAA");
        colleague3.sendData("AAA");
    }
}


```