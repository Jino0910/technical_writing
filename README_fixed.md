Swift Style Guide (코드 컨벤션)
=================

![Swift](https://img.shields.io/badge/Swift-5.0-orange.svg)

## 개요
본 문서는 iOS팀이 함께 개발할때 코드의 일관성을 유지하기 위한 스타일 가이드입니다.  
일관성이 유지된 코드는 협업하는 다른 개발자가 보더라도 문법보다 로직에 집중할 수 있는 읽기 쉬운코드가 됩니다.

iOS팀에서 작성중인 해당 문서는 코드 컨벤션을 도입하는 외부 iOS팀에게 좋은 초안이 될 수 있습니다

[관련 문서]
- [Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines)
- [Swift Style Guide](https://google.github.io/swift/)

## 목차

- [1. Swift?](#1-Swift?)
- [2. 코드 레이아웃](#2-코드-레이아웃)
    - [2.1 들여쓰기 및 띄어쓰기](#21-들여쓰기-및-띄어쓰기)
    - [2.2 줄바꿈](#22-줄바꿈)
    - [2.3 후행 쉼표](#23-후행-쉼표)
    - [2.4 최대 줄 길이](#24-최대-줄-길이)
    - [2.5 빈 줄](#25-빈-줄)
    - [2.6 임포트](#26-임포트)
- [3. 네이밍](#3-네이밍)
    - [3.1 파일네임](#31-파일네임)
    - [3.2 클래스](#32-클래스)
    - [3.3 함수](#33-함수)
    - [3.4 변수](#34-변수)
    - [3.5 상수](#35-상수)
    - [3.6 Property](#36-Property)
    - [3.7 열거형](#37-열거형)
    - [3.8 약어](#38-약어)
    - [3.9 Delegate](#39-delegate)
- [4. 코드 스타일](#4-코드-스타일)
  - [4.1 클로저](#41-클로저)
  - [4.2 클래스와 구조체](#42-클래스와-구조체)
  - [4.3 타입](#43-타입)
  - [4.4 주석](#44-주석)
- [5. 부록](#5-부록)
  - [프로그래밍 권장사항](#프로그래밍-권장사항)

## 1. Swift?
Apple의 iOS와 macOS를 위한 프로그래밍 언어입니다. 기존의 애플 운영 체제용 언어인 Objective-C와 같이 사용하기 위해 만들어졌습니다.  
따라서 Objective-C와 동일하게 LLVM(컴파일러)를 통해 빌드가 되고 같은 런타임을 공유합니다.  
Objective-C에는 없던 기능이 추가되었습니다.(클로저, 다중 리턴 타입, 네임스페이스, 제너릭, 타입 유추 등)  
Apple이 공개한 언어적 특징으로는 안정성, 신속성, 표현성입니다 그리고 객체지향, 함수형, 프로토콜지향 프로그래밍 패러다임을 차용한 프로그래밍 언어입니다

<img width="100%" src="https://user-images.githubusercontent.com/25897138/172535490-a47d6858-46d3-4501-bb2e-800eb7597dcd.jpeg">  

## 2. 코드 레이아웃 
코드의 들여쓰기, 띄어쓰기, 줄바꿈등 코드의 포맷에 대한 가이드입니다  

### 2.1 들여쓰기 및 띄어쓰기

- 들여쓰기에는 탭(tab)을 사용합니다.
- 콜론(`:`)을 쓸 때에는 콜론의 오른쪽에만 공백을 둡니다.

    ```swift
    let names: [String: String]?
    ```

  
  
### 2.2 줄바꿈

- 함수의 인자가 1개일 경우에는 아래와 같이 줄바꿈합니다.

    ```swift
    func configure(data: Data) {
        // doSomething()
    }
    ```

- 함수의 인자가 2개 이상일 경우에는 아래와 같이 줄바꿈합니다.

    ```swift
    func collectionView(
        _ collectionView: UICollectionView,      
        cellForItemAt indexPath: IndexPath       
    ) -> UICollectionViewCell {
        // doSomething()
    }

    func animationController(
        forPresented presented: UIViewController,
        presenting: UIViewController,
        source: UIViewController
    ) -> UIViewControllerAnimatedTransitioning? {
        // doSomething()
    }
    ```

- 함수의 인자가 1개일 경우에는 아래와 같이 줄바꿈합니다.

    ```swift
    let button = UIButton(type: .system)
    ```

- 함수의 인자가 2개 이상일 경우에는 파라미터 이름을 기준으로 줄바꿈합니다.

    ```swift
    let actionSheet = UIActionSheet(
        title: "정말 계정을 삭제하실 건가요?",
        delegate: self,
        cancelButtonTitle: "취소",
        destructiveButtonTitle: "삭제해주세요"
    )
    ```

    단, 파라미터에 클로저가 2개 이상 존재하는 경우에는 무조건 내려쓰기합니다.

    ```swift
    UIView.animate(
        withDuration: 0.25,
        animations: {
            // doSomething()
        }, 
        completion: { finished in
            // doSomething()
        }
    )
    ```

- `if let` 구문이 2가지 이상일 경우에는 줄바꿈하고 한 칸 들여씁니다.

    ```swift
    if let user = self.veryLongFunctionNameWhichReturnsOptionalUser(),
        let name = user.veryLongFunctionNameWhichReturnsOptionalName(),
        user.gender == .female {
      // ...
    } else {    // 이전 컨텍스트의 맺음 과 다음 컨텍스트의 시작은 한줄에 표현
        
    }
    ```
    
- `guard let` 구문이 2가지 이상일 경우에는 줄바꿈하고 한 칸 들여씁니다. `else`는 `guard`와 같은 들여쓰기를 적용합니다.

    ```swift
    guard let user = self.veryLongFunctionNameWhichReturnsOptionalUser(),
        let name = user.veryLongFunctionNameWhichReturnsOptionalName(),
        user.gender == .female
    else { // 이전 컨텍스트의 맺음 과 다음 컨텍스트의 시작은 한줄에 표현
        return 
    }
    ```


### 2.3 후행 쉼표
- 각 요소가 자체 줄에 배치되면 배열 및 사전 리터럴의 후행 쉼표가 필요합니다 . 이렇게하면 나중에 해당 리터럴에 항목을 추가 할 때 더러워집니다

    ```swift
    let configurationKeys = [
        "bufferSize",
        "compression",
        "encoding",             // ✅ GOOD.
    ]
    ```

    ```swift
    let configurationKeys = [
        "bufferSize",
        "compression",
        "encoding"              // ⛔️ AVOID.
    ]
    ```

### 2.4 최대 줄 길이

- 제약사항 없음


### 2.5 빈 줄

- 빈 줄에는 공백이 포함되지 않도록 합니다.
- 모든 파일은 빈 줄로 끝나도록 합니다.
- MARK 구문 위와 아래에는 공백이 필요합니다.

    ```swift
    // MARK: Layout

    override func layoutSubviews() {
        // doSomething()
    }

    // MARK: Actions

    override func menuButtonDidTap() {
        // doSomething()
    }
    ```
    
### 2.6 임포트

모듈 임포트는 알파벳 순으로 정렬합니다. 내장 프레임워크를 먼저 임포트하고, 빈 줄로 구분하여 서드파티 프레임워크를 임포트합니다.

```swift
import UIKit

import SwiftyColor
import SwiftyImage
import Then
import URLNavigator
```

## 3. 네이밍

### 3.1 파일네임

- 단일 유형을 포함하는 파일의 MyType이름은 MyType.swift입니다.
- MyType프로토콜에 적합성을 추가 하는 유형에 대한 단일 확장자를 포함하는 파일의 MyProtocol이름은 MyType+MyProtocol.swift입니다.
- 형식에 여러 가지 확장자를 포함하는 파일 MyType은 형식에 접두사, 중첩 형식 또는 기타 기능을 추가하는 것이 더 일반적입니다 MyType+. 예를 들면 다음과 같습니다 MyType+Extensions.swift.
- 공통 유형 또는 네임 스페이스 (예 : 전역 수학 함수 모음)로 범위가 지정되지 않은 관련 선언이 포함 된 파일은 설명 적으로 이름을 지정할 수 있습니다. 예를 들면 다음과 같습니다 Math.swift.


### 3.2 클래스

- 클래스 이름에는 UpperCamelCase를 사용합니다.
- 클래스 이름에는 접두사<sup>Prefix</sup>를 붙이지 않습니다.

### 3.3 함수

- 함수 이름에는 lowerCamelCase를 사용합니다.
- 함수 이름 앞에는 되도록이면 `get`을 붙이지 않습니다.

    **✅ 좋은 예:**

    ```swift
    func name(for user: User) -> String?
    ```

    **⛔️ 나쁜 예:**

    ```swift
    func getName(for user: User) -> String?
    ```

- Action 함수의 네이밍은 '주어 + 동사 + 목적어' 형태를 사용합니다.

    - *Tap(눌렀다 뗌)*은 `UIControlEvents`의 `.touchUpInside`에 대응하고, *Press(누름)*는 `.touchDown`에 대응합니다.
    - *will~*은 특정 행위가 일어나기 직전이고, *did~*는 특정 행위가 일어난 직후입니다.
    - *should~*는 일반적으로 `Bool`을 반환하는 함수에 사용됩니다.

    **✅ 좋은 예:**

    ```swift
    func backButtonDidTap() {
        // ...
    }
    ```

    **⛔️ 나쁜 예:**

    ```swift
    func back() {
        // ...
    }

    func pressBack() {
        // ...
    }
    ```

### 3.4 변수

- 변수 이름에는 lowerCamelCase를 사용합니다.

### 3.5 상수

- 상수 이름에는 lowerCamelCase를 사용합니다.

    **✅ 좋은 예:**

    ```swift
    let maximumNumberOfLines = 3
    ```

    **⛔️ 나쁜 예:**

    ```swift
    let kMaximumNumberOfLines = 3
    let MAX_LINES = 3
    ```

### 3.6 Property

- 선언 형식의 인스턴스를 반환하는 정적 및 클래스 속성에는 이름이 접미사로 붙지 않습니다.

    **✅ 좋은 예:**
    ```swift
    public class UIColor {
        public class var red: UIColor {         // GOOD.
            // ...
        }
    }

    public class URLSession {
        public class var shared: URLSession {   // GOOD.
            // ...
        }
    }
    ```

    **⛔️ 나쁜 예:**
    ```swift
    public class UIColor {
        public class var redColor: UIColor {            // AVOID.
            // ...
        }
    }

    public class URLSession {
        public class var sharedSession: URLSession {    // AVOID.
            // ...
        }
    }
    ```
    
### 3.7 열거형

- enum의 각 case에는 lowerCamelCase를 사용합니다.

    **✅ 좋은 예:**

    ```swift
    enum Result {
        case success
        case failure
    }
    ```
    
    **⛔️ 나쁜 예:**

    ```swift
    enum Result {
        case Success
        case Failure
    }
    ```

- 다음 예에서 사례는 기본 HTTP 상태 코드를 기반으로 숫자 순서로 정렬되며 빈 줄은 그룹을 구분하는 데 사용됩니다.

    ```swift
    public enum HTTPStatus: Int {  // ✅ GOOD.
        case ok = 200

        case badRequest = 400
        case notAuthorized = 401
        case paymentRequired = 402
        case forbidden = 403
        case notFound = 404

        case internalServerError = 500
    }
    ```
- 같은 열거 형의 다음 버전은 읽기가 어렵습니다. 사건이 사전 식으로 정렬되었지만 관련 값의 의미있는 그룹이 손실되었습니다.

    ```swift
    public enum HTTPStatus: Int { // ⛔️ AVOID.
        case badRequest = 400
        case forbidden = 403
        case internalServerError = 500
        case notAuthorized = 401
        case notFound = 404
        case ok = 200
        case paymentRequired = 402
    }
    ```





### 3.8 약어

- 약어로 시작하는 경우 소문자로 표기하고, 그 외의 경우에는 항상 대문자로 표기합니다.

    **✅ 좋은 예:**

    <pre>
    let user<strong>ID</strong>: Int?
    let <strong>html</strong>: String?
    let website<strong>URL</strong>: URL?
    let <strong>url</strong>String: String?
    </pre>

    **⛔️ 나쁜 예:**

    <pre>
    let user<strong>Id</strong>: Int?
    let <strong>HTML</strong>: String?
    let website<strong>Url</strong>: NSURL?
    let <strong>URL</strong>String: String?
    </pre>

### 3.9 Delegate

- Delegate 메서드는 프로토콜명으로 네임스페이스를 구분합니다.

    **✅ 좋은 예:**

    ```swift
    protocol UserCellDelegate {
        func userCellDidSetProfileImage(_ cell: UserCell)
        func userCell(_ cell: UserCell, didTapFollowButtonWith user: User)
    }
    ```

    **⛔️ 나쁜 예:**

    ```swift
    protocol UserCellDelegate {
        func didSetProfileImage()
        func followPressed(user: User)
    }
    ```
## 4. 코드 스타일

### 4.1 클로저

- 파라미터와 리턴 타입이 없는 Closure 정의시에는 `() -> Void`를 사용합니다.

    **✅ 좋은 예:**

    ```swift
    let completionBlock: (() -> Void)?
    ```

    **⛔️ 나쁜 예:**

    ```swift
    let completionBlock: (() -> ())?
    let completionBlock: ((Void) -> (Void))?
    ```

- Closure 정의시 파라미터에는 괄호를 사용하지 않습니다.

    **✅ 좋은 예:**

    ```swift
    { operation, response in
        // doSomething()
    }
    ```

    **⛔️ 나쁜 예:**

    ```swift
    { (operation, responseObject) in
        // doSomething()
    }
    ```

- Closure 정의시 가능한 경우 타입 정의를 생략합니다.

    **✅ 좋은 예**

    ```swift
    ...,
    completion: { finished in
        // doSomething()
    }
    ```

    **⛔️ 나쁜 예:**

    ```swift
    ...,
    completion: { (finished: Bool) -> Void in
        // doSomething()
    }
    ```

- Closure 호출시 또다른 유일한 Closure를 마지막 파라미터로 받는 경우, 파라미터 이름을 생략합니다.

    **✅ 좋은 예:**

    ```swift
    UIView.animate(withDuration: 0.5) {
        // doSomething()
    }
    ```

    **⛔️ 나쁜 예:**

    ```swift
    UIView.animate(withDuration: 0.5, animations: { () -> Void in
        // doSomething()
    })
    ```



- 후행 종결 구문으로 호출 된 함수가 다른 인수를 취하지 않으면 ()함수 이름 뒤에 빈 괄호 ( )가 존재 하지 않습니다 .

    **✅ 좋은 예:**
    
    ```swift
    let squares = [1, 2, 3].map { $0 * $0 }
    ```

    **⛔️ 나쁜 예:**

    ```swift
    let squares = [1, 2, 3].map({ $0 * $0 })
    let squares = [1, 2, 3].map() { $0 * $0 }
    ```



### 4.2 클래스와 구조체

- 클래스와 구조체 내부에서는 `self`를 명시적으로 사용합니다.

- 더이상 상속이 발생하지 않는 클래스는 항상 `final` 키워드로 선언합니다. (클래스)

- 프로토콜을 적용할 때에는 extension을 만들어서 관련된 메서드를 모아둡니다.

    **✅ 좋은 예:**

    ```swift
    final class MyViewController: UIViewController {
        // ...
    }

    // MARK: - UITableViewDataSource

    extension MyViewController: UITableViewDataSource {
        // ...
    }

    // MARK: - UITableViewDelegate

    extension MyViewController: UITableViewDelegate {
        // ...
    }
    ```

    **⛔️ 나쁜 예:**

    ```swift
    final class MyViewController: UIViewController, UITableViewDataSource, UITableViewDelegate {
      // ...
    }
    ```

### 4.3 타입

- `Array<T>`와 `Dictionary<T: U>` 보다는 `[T]`, `[T: U]`를 사용합니다.

    **✅ 좋은 예:**

    ```swift
    var messages: [String]?
    var names: [Int: String]?
    ```

    **⛔️ 나쁜 예:**

    ```swift
    var messages: Array<String>?
    var names: Dictionary<Int, String>?
    ```

### 4.4 주석

- `///`를 사용해서 문서화에 사용되는 주석을 남깁니다.

    ```swift
    /// 사용자 프로필을 그려주는 뷰
    class ProfileView: UIView {

        /// 사용자 닉네임을 그려주는 라벨
        var nameLabel: UILabel!
    }
    ```


- `// MARK:`를 사용해서 연관된 코드를 구분짓습니다.

    Objective-C에서 제공하는 `#pragma mark`와 같은 기능으로, 연관된 코드와 그렇지 않은 코드를 구분할 때 사용합니다.

    ```swift
    // MARK: Init

    override init(frame: CGRect) {
        // doSomething()
    }

    deinit {
        // doSomething()
    }


    // MARK: Layout

    override func layoutSubviews() {
        // doSomething()
    }


    // MARK: Actions

    override func menuButtonDidTap() {
        // doSomething()
    }
    ```

## 5. 부록

### 프로그래밍 권장사항

- 가능하다면 변수를 정의할 때 함께 초기화하도록 합니다. [Then](https://github.com/devxoul/Then)을 사용하면 초기화와 함께 속성을 지정할 수 있습니다.

    ```swift
    let label = UILabel().then {
      $0.textAlignment = .center
      $0.textColor = .black
      $0.text = "Hello, World!"
    }
    ```

- 상수를 정의할 때에는 `enum`를 만들어 비슷한 상수끼리 모아둡니다. 재사용성과 유지보수 측면에서 큰 향상을 가져옵니다. `struct` 대신 `enum`을 사용하는 이유는, 생성자가 제공되지 않는 자료형을 사용하기 위해서입니다. [CGFloatLiteral](https://github.com/devxoul/CGFloatLiteral)과 [SwiftyColor](https://github.com/devxoul/SwiftyColor)를 사용해서 코드를 단순화시킵니다.

    ```swift
    final class ProfileViewController: UIViewController {

        private enum Metric {
            static let profileImageViewLeft = 10.f
            static let profileImageViewRight = 10.f
            static let nameLabelTopBottom = 8.f
            static let bioLabelTop = 6.f
        }

        private enum Font {
            static let nameLabel = UIFont.boldSystemFont(ofSize: 14)
            static let bioLabel = UIFont.boldSystemFont(ofSize: 12)
        }

        private enum Color {
            static let nameLabelText = .h3c7ae5 
            static let bioLabelText = .h333333 ~ 70%
        }

    }
    ```

    이렇게 선언된 상수들은 다음과 같이 사용될 수 있습니다.

    ```swift
    self.profileImageView.frame.origin.x = Metric.profileImageViewLeft
    self.nameLabel.font = Font.nameLabel
    self.nameLabel.textColor = Color.nameLabelText
    ```

- 더이상 상속이 발생하지 않는 클래스는 항상 `final` 키워드로 선언합니다.

- 프로토콜을 적용할 때에는 extension을 만들어서 관련된 메서드를 모아둡니다.

    **✅ 좋은 예:**

    ```swift
    final class MyViewController: UIViewController {
        // ...
    }

    // MARK: - UITableViewDataSource

    extension MyViewController: UITableViewDataSource {
        // ...
    }

    // MARK: - UITableViewDelegate

    extension MyViewController: UITableViewDelegate {
        // ...
    }
    ```

    **⛔️ 나쁜 예:**

    ```swift
    final class MyViewController: UIViewController, UITableViewDataSource, UITableViewDelegate {
      // ...
    }
    ```
