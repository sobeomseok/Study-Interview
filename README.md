# 면접 스터디중에 내가 맡은 파트 정리

```swift

31. setNeedsLayout와 setNeedsDisplay의 차이에 대해 설명하시오.

mainrunloop는 터치이벤트,위치의변화,디바이사의 회전등 각종 이벤트들을 처리하게됩니다. 이러한 처리 과정에서 각 이벤트에 맞는 알맞는 핸들러를 찾아 그들에게 권한을 위임하고여 진행합니다.

발생한 모든 이벤트를 처리한뒤 다시 권한이 mainrunloof로 돌아오는 시점은 updte cycle 이라고 합니다.

setNeedsDisplay 메서드는 View의 컨텐츠가 변할때 시스템에 view를 다시 그려야한다는걸 시스템에게 알려줍니다. 다음 update cycle 이 오고 draw메서드가 호출되면 뷰의 업데이트들이 한번에 이루어집니다. 비동기적으로 작동합니다.

setNeedsLayout 메서드는 view의 하위뷰들의 레이아웃을 조정하고 싶을때 호출합니다. 이메서드도 또한 다음 update cycle이 올때 layoutSubviews 메서드가 호출되며 모든 업데이트들이 한번에이루어집니다. 비동기적으로 작동합니다.

결국 이 두개의 메서드의 차이점은 이렇게 정리할수 있습니다.

setNeedsDisplay 는 다음 update cycle 때 draw 메서드를 호출하게끔 시스템에 유도합니다.

그 뒤에 쌓여있는 view의 컨텐츠를 다시 그립니다

setNeedLayout 은 다음 update cycle 때 layoutSubview를 호출하게 끔 시스템에 유도합니다.

그 뒤에 view의 레이아웃의 관한 변화를 적용합니다

출처: [https://velog.io/@zeke/difference-between-setNeedsLayoutsetNeedsDisplay](https://velog.io/@zeke/difference-between-setNeedsLayoutsetNeedsDisplay)

32. NSCache와 NS딕셔너리로 캐시를 구성했을때의 차이를 설명하시오.

일단 캐시를 알아야하는데

Cache란 자주 사용하는 데이터나 값을 미리 복사해 놓는 임시 장소를 가리킨다. 아래와 같은 저장공간 계층 구조에서 확인할 수 있듯이, 캐시는 저장 공간이 작고 비용이 비싼 대신 빠른 성능을 제공한다. 라고 알고계시면 됩니다.

고용량의 데이터를 캐시에 복사해두면 아주 빠른속도로 데이터에 접근할수있는데 결국 반복적으로 데이터를 불러오는경우에는 지속적으로 서버에 요청하는것이 아닌 메모리에 데이터를 저장하였다가 불러다 쓰는것을 의미합니다

NS딕셔너리는 메모리가 부족하다는 시스템 경고를 받을때 메모리를 정리하는 코드를 미리 직접 작성해야하지만

NsCache는 자동으로 처리해줍니다.

(다른앱에서 메모리를 더 사용하려고하면 캐시되어있던 데이터를 지우고 메모리를 해제 합니다)

NsCache는 thread safe 합니다 NS딕셔너리는 그렇지 않습니다.

(캐시데이터를 읽고 쓰고 지울때마다 따로 LOCK을 해줄 필요없습니다. 딕셔너리는 데이터에 접근할때마다 따로 처리해줘야합니다)

(thread safe하지않다는것은 앨런강의 복습!)

(간단하게 한 쓰레드가 사용하는 메모리 공간에 다른 쓰레드가 접근하는것을 의미합니다)

33. URLSession에 대해서 설명하시오.

Session 이란 일정시간동안 브라우저로부터 들어오는 연결상태를 유지하는 기술이나 연결상태를 의미합니다

URLSession 은 서버와 통신하기위해 애플에서 제공하는 API입니다.

URLSession 인스턴스를 만들어 각 인스턴스들이 네트워크 통신과 관련된 작업들을 그룹지어 관리합니다.

URLSession은 HTTP를 포함한 몇가지 프로토콜을 지원하고 인증,쿠키,관리,캐시 등을 지원합니다.

또한 URLSession을 통해서 앱이 실행되고있지 않아도 백그라운드에서 다운로드를 진행할 수 있게 도와줍니다.

1. prepareForReuse에 대해서 설명하시오.

테이블를 사용할때 테이블뷰셀을 재사용하는 경우가 많습니다.

셀을 재사용하기 때문에 재사용된 셀에서 보여줄필요없는 텍스트나 버튼등이 보여지는 경우가있습니다.

그렇기때문에 재사용된 셀을 사용할때는 반드시 모든값이 초기화 되어져야 합니다.

그리고 이렇게 초기화를 하기위해 호출하는 함수를 말합니다.

35. 다크모드를 지원하는 방법에 대해 설명하시오.

1. ****Assets Catalog 에 color set을 사용하여 각 모드에 맞는 컬러를 설정해줄수있습니다****

1. UITraitCollection.userinteerfaceStyle을 이용해 현재 어떤 모드인지 알수있고 그 모드에 따른 색을 설정해줄수 있습니다.

1. systemColor를 사용하면 자동으로 다크모드를 지원해줍니다 ㅎㅎ

36. ViewController의 생명주기를 설명하시오. 

요건 저번주에 설명 했쬬잉?

37. TableView와 CollectionView의 차이점을 설명하시오.

컬렉션뷰는 테이블뷰에서 구현할 수 있는 모든것을 할수 있습니다.

컬렉션뷰는 여러개의 열과 행으로 셀을  표현할 수 있습니다. 그래서 수직 스크롤 뿐만 아니라 수평스크롤도 할수 있습니다.

테이블뷰는 하나의 열에 여러 행을 표시하는 형식이기때문에 셀의 디자인을 행에 맞춰서 디자인합니다.

컬렉션뷰는 열과 행을 만들수 있기 때문에 꼭 행의 모습이 아니더라도 다양한 모습으로 셀을 디자인 할수 있습니다.

또한 컬렉션뷰의 가장 큰 기능은 레이아웃입니다.

이는 곧 한화면에 다양한 모습의 셀을 가진 뷰를 만들수 있다는 뜻이기도합니다.

테이블뷰는 간단하고 보편적인 목록을 만들고 디자인 변경이 없을때 사용하고

컬렉션뷰는 특정한 모습의 목록을 만들고 나중에 디자인도 바뀔수 있을때 사용 합니다

출처 :[http://labs.brandi.co.kr/2018/05/02/kimjh.html](http://labs.brandi.co.kr/2018/05/02/kimjh.html)

38. 오토레이아웃을 코드로 작성하는 방법은 무엇인가? (3가지)

1. NSLayoutConstraint


NSLayoutConstraint(item: myView, attribute: .leading, relatedBy: .equal, toItem: view, attribute: .leadingMargin, multiplier: 1.0, constant: 0.0).isActive = true
 
NSLayoutConstraint(item: myView, attribute: .trailing, relatedBy: .equal, toItem: view, attribute: .trailingMargin, multiplier: 1.0, constant: 0.0).isActive = true
 
NSLayoutConstraint(item: myView, attribute: .height, relatedBy: .equal, toItem: myView, attribute:.width, multiplier: 2.0, constant:0.0).isActive = true


이 방법은 레이아웃에 영향을 주지 않더라도 각 매게 변수에 대한 값을 지정해야합니다.

1. ****Anchors****


myView.trailingAnchor.constraint(equalTo: margins.trailingAnchor).isActive = true


이 방법이 권장됨.

****3. Visual Format Language****


let views: [String : Any] = ["a": aView,
                                     "b": bView]
        let format1 = "H:|-[a]-|"
        let format2 = "H:|-30-[b]-30-|"
        let format3 = "V:|-20-[a(100)]"
        let format4 = "V:[a]-20-[b(100)]"
        
        var constraint = NSLayoutConstraint.constraints(withVisualFormat: format1,
                                                        options: [],
                                                        metrics: nil,
                                                        views: views)
        constraint += NSLayoutConstraint.constraints(withVisualFormat: format2,
                                                     options: [],
                                                     metrics: nil,
                                                     views: views)
        constraint += NSLayoutConstraint.constraints(withVisualFormat: format3,
                                                     options: [],
                                                     metrics: nil,
                                                     views: views)
        constraint += NSLayoutConstraint.constraints(withVisualFormat: format4,
                                                     options: [],
                                                     metrics: nil,
                                                     views: views)
        view.addConstraints(constraint)


NSLayoutConstraint 방법보단 알기 쉬워졌지만 문법이 어려워 잘 사용하지않음

1. hugging, resistance에 대해서 설명하시오.

둘다 뷰의 우선순위를 결정하는 속성입니다

hugging 은 우선순위가 클수록 자신의 크기를 유지하려하고, 우선순위가 작을수록 크기가 늘어나는 속성을 말하고,

resistance 는 우선순위가 클수록 자신의 크기를 유지하려하고, 우선순위가 작을수록 크기가 작아지려는 속성을 말합니다.

예를 들어 두개의 뷰가 서로 붙어있고 그 크기가 지정되지 않은 상태에서 우선순위가 없다면 hugging 이 클수록 작게, resistance 가 클수록 너비를 크게 가지게 됩니다.

출처: [https://eunjin3786.tistory.com/43](https://eunjin3786.tistory.com/43)

40. Intrinsic Size에 대해서 설명하시오.

Intrinsic Size는 콘텐츠의 본질적인 크기입니다.

모든 view가 Intrinsic Size를 갖는 것은 아니고, 대표적인 예로는 UILabel, UIButton을 들 수 있습니다.

UILable 이나 UIButton의 오토레이아웃을 구현할때 높이height와 너비width를 설정해주지않아도 오류가나지않는 이유가 바로 intrinsic size를 가지고 있기 때문입니다

 

1. 스토리보드를 이용했을때의 장단점을 설명하시오.

스토리보드의 장점은 

결과물이 직접적으로 눈 에 보입니다 그렇기 때문에 코드를 하나하나 확인해보지 않아도 파악이 가능합니다.

오토레이아웃을 코드로 하는것보다 쉽습니다. 그렇기 때문에 진입장벽이 낮아 초보자도 쉽게 사용할수 있다는 점입니다 

많은 코드를 작성하지않아도 앱의 디자인과 뷰의 이동,전환을 쉽게 조종할수 있습니다.

스토리보드의 단점은

스토리보드는 무겁기때문에 앱이 점점 커질수록 스토리보드 로딩시간이 길어집니다.

스토리보드로 만든 뷰는 재사용성이 떨어집니다.

다른개발자들과 협업하는 경우 병합충돌이 일어납니다.그리고 해결하기 매우 어렵습니다

스토리보드는 뷰의 이동은 처리하지만 데이터의 이동은 처리하지 못합니다.

42. Safearea에 대해서 설명하시오.

아이폰 X 부터 나온 개념으로, M자 탈모 아이폰이 등장하면서 상단의 노치와 하단의 홈바에는 콘텐츠가 제대로 표시되지 않기 때문에, 이 부분을 제외하고 **콘텐츠가 안전하게 표시될 수 있는 영역**
을 의미합니다.

43. Left Constraint 와 Leading Constraint 의 차이점을 설명하시오.

`Left Constraint`는 어떤 객체의 왼쪽을 뜻하고, `Leading Constraint`는 어떤 객체의 앞쪽 가장자리를 뜻합니다.

한국어는 왼쪽 부터 오른쪽으로 쓰여 나갑니다 그렇기 때문에 leading은 왼쪽입니다.

하지만 아랍어는 오른쪽부터 왼쪽으로 쓰여나갑니다 그렇기때문에 leading 오른쪽입니다.

애플에서는 left right보다 leading trailing을 권장합니다

출처: [https://babbab2.tistory.com/133](https://babbab2.tistory.com/133)

44. struct와 class와 enum의 차이를 설명하시오.

열거형은 같은성질을 가지는것들에 대한 목록을 case별로 나열한것입니다.

열거형은 값타입이며 상속이 불가능하고 확장이 가능합니다

구조체는 

여러 변수를 담을 수 있는 컨테이너 개념으로

데이터를 용도에 맞게 묶어 표현할 때 용이합니다.

값타입이며 상속이 불가능하고 확장이 가능합니다.

실제 인스턴스의 데이터 자체가 스택에 저장됨

swift의 큰틀은 대부분 구조체로 구성되어있습니다(ex: string , int)

클래스 또한 여러변수를 담을수 있는 컨테이너 개념이며

참조타입이고 상속과 확장이 모두 가능합니다

실제 인스턴스(데이터)는 힙에 저장되고, 그 인스턴스를 가리키는 변수에 메모리 주소가 담겨 스택에 저장됩니다.

ios 프레임워크의 대부분은 클래스로 구성되어있습니다(uiviewcontroller, uibutton)

1. class의 성능을 향상 시킬수 있는 방법들을 나열해보시오.

출처: [https://babbab2.tistory.com/145](https://babbab2.tistory.com/145) 에 이유가 자세히 설명되어있습니다

****상속, 오버라이딩 될 필요가 없는 클래스, 메서드, 프로퍼티에 final 키워드 붙이기****

****접근이 현재 파일로 제한되는 경우 private 키워드 붙이기****

****WMO(Whole Module Optimization) 사용하기****



```
