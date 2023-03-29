## TDD(Test Driven Development)


#### TDD : 테스트 주도 개발
'테스트가 개발을 이끌어 나간다.'

짧은 개발 주기의 반복에 의존하는 개발 프로세스이며,
애자일 방법론 중 하나인 eXtream Programming(XP)의 'Test-First' 개념에 기반을 둔 단순한 설계를 중요시

**eXtream Programming(XP)**
> 미래에 대한 예측을 최대한 하지 않고, 지속적으로 프로토타입을 완성하는 애자일 방법론 중 하나.
이 방법론은 추가 요구사항이 생기더라도, 실시간으로 반영할 수 있다. 
</br>

### TDD 개발주기

![image](https://user-images.githubusercontent.com/32945436/228411439-d32e4422-0ed7-4573-a5c0-0238e433a7a9.png) </br>

**Red** 단계는 **실패하는 테스트 코드** 작성 </br>
**Green** 단계는 **테스트 코드를 성공시키기 위한 실제 코드** 작성 </br>
**Blue** 단계는 중복 코드 제거, 일반화 등의 **리팩토링**을 수행 </br> 
</br> 
</br> 
중요한 건 **Red** 단계가 끝날 때 까지 **실제코드**를 작성하지 않고 **Green** 단계에서 테스트 코드를 통과할 정도의 최소 실제 코드만 작성하는 것이다.

![image](https://user-images.githubusercontent.com/32945436/228412034-e8a0818b-2aaa-4880-b426-8b1664d49e25.png)




## 일반 개발 vs TDD
### 일반 개발
![img](https://mblogthumb-phinf.pstatic.net/MjAxNzA2MjhfMTU0/MDAxNDk4NjA2NTAyNjU2.zKGh5ZuYgToTz6p1lWgMC_Xb30i7uU86Yh00N2XrpMwg.8b3X9cCS6_ijzWyXEiQFombsWM1J8FlU9LhQ2j0nanog.PNG.suresofttech/image.png?type=w800)
<br>
보통의 개발 방식은 '요구사항 분석 -> 설계 -> 개발 -> 테스트 -> 배포'의 형태의 개발 주기를 갖는데 <br>
이러한 방식은 소프트웨어 개발을 느리게 하는 잠재적 위험이 존재한다. <br>
하지만 TDD는 기존 방법과는 다르게, 테스트케이스를 먼저 작성한 이후에 실제 코드를 개발하는 리팩토링 절차를 밟는다.
- 처음부터 명확하지 않을 수 있다.
- 완벽한 설계는 어렵기 때문에
- 디버깅하기 어려워서 소스코드 품질이 저하
- 그래서 테스트 비용이 증가한다.
<br>
<br>

### TDD
![img](https://mblogthumb-phinf.pstatic.net/MjAxNzA2MjhfMjE3/MDAxNDk4NjA2NTExNDgw.fp8XF9y__Kz75n86xknIPDthTHj9a8Q08ocIJIqMR6Ag.24jJa_8_T0Qj04P62FZbchqt8oTNXGFSLUItzMP95s8g.PNG.suresofttech/image.png?type=w800)
<br>
테스트 코드를 작성한 뒤에 실제 코드를 작성한다는 것이다. <br>
무엇을 테스트해야 할지 미리 정의해야 하는 것이다.
- 예외사항들은 테스트 케이스 추가하고 설계를 개선한다.
- 통과한 것들을 실제코드로 작성
<br>

##### 장점

작업과 동시에 테스트를 진행하면서 실시간으로 오류 파악이 가능 ( 시스템 결함 방지 )

짧은 개발 주기를 통해 고객의 요구사항 빠르게 수용. 피드백이 가능하고 진행 상황 파악이 쉬움

테스트 단위 프레임워크를 사용해서 소스코드 간결해짐

(자바는 JUnit, C와 C++은 CppUnit 등)

개발자가 기대하는 앱의 동작에 관한 문서를 테스트가 제공해줌 <br>
`또한 이 테스트 케이스는 코드와 함께 업데이트 되므로 문서 작성과 거리가 먼 개발자에게 매우 좋음`

##### 단점

기존 개발 프로세스에 테스트케이스 설계가 추가되므로 생산 비용 증가

테스트의 방향성, 프로젝트 성격에 따른 테스트 프레임워크 선택 등 추가로 고려할 부분의 증가

<br>
<br>
<br>

#### 점수 계산 프로그램을 통한 TDD 예제 진행

---

중간고사, 기말고사, 과제 점수를 통한 성적을 내는 간단한 프로그램을 만들어보자

점수 총합 90점 이상은 A, 80점 이상은 B, 70점 이상은 C, 60점 이상은 D, 나머지는 F다.

<br>

TDD 테스트케이스를 먼저 작성한다.

35 + 25 + 25 = 85점이므로 등급이 B가 나와야 한다.

따라서 assertEquals의 인자값을 "B"로 주고, 테스트 결과가 일치하는지 확인하는 과정을 진행
<br>
```java
public class GradeTest {
    
    @Test
    public void scoreResult() {
        
        Score score = new Score(35, 25, 25); // Score 클래스 생성
        SimpleScoreStrategy scores = new SimpleScoreStrategy();
        
        String resultGrade = scores.computeGrade(score); // 점수 계산
        
        assertEquals("B", resultGrade); // 확인
    }
    
}
```
<br>
<br>

현재는 **Score 클래스와 computeGrade() 메소드가 구현되지 않은 상태**다. (테스트 코드로만 존재)

테스트 코드에 맞춰서 코드 개발을 진행
<br>
<br>

우선 점수를 저장할 Score 클래스를 생성한다
<br>
````java
public class Score {
    
    private int middleScore = 0;
    private int finalScore = 0;
    private int homeworkScore = 0;
    
    public Score(int middleScore, int finalScore, int homeworkScore) {
        this.middleScore = middleScore;
        this.finalScore = finalScore;
        this.homeworkScore = homeworkScore;
    }
    
    public int getMiddleScore(){
        return middleScore;
    }
    
    public int getFinalScore(){
        return finalScore;
    }
    
    public int getHomeworkScore(){
        return homeworkScore;
    }
    
}
````
<br>
<br>

이제 점수 계산을 통해 성적을 뿌려줄 computeGrade() 메소드를 가진 클래스를 만든다.

<br>

우선 인터페이스를 구현하자
<br>
```java
public interface ScoreStrategy {
    
    public String computeGrade(Score score);
    
}
```

<br>

인터페이스를 가져와 오버라이딩한 클래스를 구현한다
<br>
```java
public class SimpleScoreStrategy implements ScoreStrategy {
    
    public String computeGrade(Score score) {
        
        int totalScore = score.getMiddleScore() + score.getFinalScore() + score.getHomeworkScore(); // 점수 총합
        
        String gradeResult = null; // 학점 저장할 String 변수
        
        if(totalScore >= 90) {
            gradeResult = "A";
        } else if(totalScore >= 80) {
            gradeResult = "B";
        } else if(totalScore >= 70) {
            gradeResult = "C";
        } else if(totalScore >= 60) {
            gradeResult = "D";
        } else {
            gradeResult = "F";
        }
        
        return gradeResult;
    }
    
}
```
<br>
<br>

이제 테스트 코드로 돌아가서, 실제로 통과할 정보를 입력해본 뒤 결과를 확인해보자

이때 예외 처리, 중복 제거, 추가 기능을 통한 리팩토링 작업을 통해 완성도 높은 프로젝트를 구현할 수 있도록 노력하자!

<br>

통과가 가능한 정보를 넣고 실행하면, 아래와 같이 에러 없이 제대로 실행되는 모습을 볼 수 있다.
<br>
<br>

![img](https://mblogthumb-phinf.pstatic.net/MjAxNzA2MjhfMjQx/MDAxNDk4NjA2NjM0MzIw.LGPVpvam5De7ibWipMqiGHZPjRcKWQKYhLbKgnL6i78g.8vplllDO1pfKFs5Wua9ZLl7b6g6kHbjG-6M--HmDRCwg.PNG.suresofttech/image.png?type=w800)

<br>
<br>


***굳이?***

TDD를 활용하면, 처음 시작하는 단계에서 테스트케이스를 설계하기 위한 초기 비용이 확실히 더 들게 된다.
하지만 개발 과정에 있어서 '초기 비용'보다 '유지보수 비용'이 더 클 수 있기 때문에 생각하는 것

[참고자료] https://inpa.tistory.com/entry/QA-%F0%9F%93%9A-TDD-%EB%B0%A9%EB%B2%95%EB%A1%A0-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%A3%BC%EB%8F%84-%EA%B0%9C%EB%B0%9C#tdd%EC%9D%98_%EB%8B%A8%EC%A0%90

