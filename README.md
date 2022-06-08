# 졸업작품(캡스톤)

# capstone22

**팀명: 스윗프트(sweetft) <br>
이름: 강재혁(App-)** <br>
**졸업작품 소개 사이트:https://kang-jae-heok.github.io/SweetftWeb//** <br> 
**포트폴리오 소개 사이트:**

### [졸업작품 소개]

**작품명: Bbetter**

**개발환경: SWIFT** 

**작품 소개: 더 편리하고 나은 생활을 보조하는 데일리 어플이다. 주요 기능은 목표설정, 일기 및 메모, 날씨, 뉴스가 있다.** 

**작품의 특징:크롤링을 이용하여 뉴스를 출력**

## [05/18]
realmSwift :Realm은 모바일에 특화된 NoSQL 데이터베이스 <br>
대표적인 특징으로는 ORM이 아닌 데이터 컨테이너 모델을 사용하고, 데이터 객체를 Realm에 객체 형태로 저장합니다. 그렇기 때문에 DB에서 가져온 데이터를 복잡한 가공과정 없이 바로 사용할 수 있다는 장점이 있습니다. <br>

```pod 'RealmSwift', '~>10'
pod install
```

swiftsoup:  웹 크롤링을 할 수 있게 하는 라이브러리입니다.

```let imagesrc: Elements = try doc.select("div#carMainImgArea.img_group").select("div.main_img").select("img[src]")

let stringImage = try imagesrc.attr("src").description

let urlImage = URL(string: stringImage)


let data = try Data(contentsOf: urlImage!)

carImage.image = UIImage(data: data) // UI 세팅
```

```
class Phonebook: Object {
    @Persisted(PrimaryKey: true) var number: String? // primary key로 지정
    @Persisted var name: String = ""
    @Persisted var status: String = ""

    convenience init(number: String) {
        self.init()
        self.number = number
    }
}
```


## [05/18]
캘린더 일기 

```swift
class CalenderViewController: UIViewController {
    
    @IBOutlet weak var itemLabel: UILabel!
    @IBOutlet weak var datePicker: UIDatePicker!
    
    var date = dateFormatter.string(from: Date())
    
    
    private let realm = try! Realm()
 
    static let dateFormatter: DateFormatter = {
        let dateFormatter = DateFormatter()
        dateFormatter.dateFormat = "yyyy/MM/dd"
        return dateFormatter
    }()
    

    override func viewWillAppear(_ animated: Bool) {
        let list = realm.objects(diaryItem.self).filter("date == '\(date)'")
        for item2 in list{
            itemLabel?.text! = "\(item2.item)"
        }
    }

    override func viewDidLoad() {
        super.viewDidLoad()
        
        let list = realm.objects(diaryItem.self).filter("date == '\(date)'")
        for item2 in list{
            itemLabel?.text! = "\(item2.item)"
        }

        let tap = UITapGestureRecognizer(target: self, action: #selector(CalenderViewController.tapItemLabel))
        itemLabel.isUserInteractionEnabled = true
        itemLabel.addGestureRecognizer(tap)

    }
    
    @objc func tapItemLabel(sender:UITapGestureRecognizer){
        
        guard let vc = storyboard?.instantiateViewController(identifier: "view") as? CalenderViewViewController else{
            return
        }
        vc.dataDate = date
        vc.navigationItem.largeTitleDisplayMode = .never
      
        navigationController?.pushViewController(vc, animated: true)
        
     
        
        }
    
    @IBAction func didDatePickerValueChanged(_ sender: UIDatePicker){
       
        self.date = Self.dateFormatter.string(from: datePicker!.date)
        let list = realm.objects(diaryItem.self).filter("date == '\(date)'")
        
        if list.count == 0{
            itemLabel?.text! = "내용을 입력해주세요"
        }else{
            for item2 in list{
                itemLabel?.text! = "\(item2.item)"
            }
        }

    }
```

## [05/04]
json 파싱을 하기위한 구조체

```swift
struct Papago: Codable {
        let message: Message
    }
    struct Message: Codable {
        let result: Result
    }
    struct Result: Codable{
        let translatedText: String
        let srcLangType: String
        let tarLangType: String
    }
```

```swift
if error == nil && data != nil {
                let decoder = JSONDecoder()
                do{
                    let decodedData = try decoder.decode(Papago.self, from: data!)
                    
                    print(decodedData)
                    DispatchQueue.main.async {
                        self.textLabel.text = decodedData.message.result.translatedText
                        
                    }
                }catch{
                    print("error")
                }
            }
            //통신 실패
            if let error = error {
                print(error.localizedDescription)
            }
        }
        task.resume()
    }
```

json 파싱

### [04/13]
데이트 피커를 이용한 캘린더 작업
```
class DateViewController: UIViewController {
    @IBOutlet weak var datePicker: UIDatePicker!
    let dateFormatter: DateFormatter = {
        let formatter: DateFormatter = DateFormatter()
        formatter.dateFormat = "yyy/MM/dd"
        return formatter
    }()
    
    override func viewDidLoad() {
        super.viewDidLoad()

        // Do any additional setup after loading the view.
    }
    
```
데이트피커를 상속받아 IBOutlet을 만들고 날짜를 받아온다

### [04/06]
기획서 알람,뉴스,쪽을 마무리 함 <br>
깃 크라켄 연결, 브랜치 생성 및 깃 프로 계정 전환 <br>
xcode 에서 텝바로 기초적인 화면 구성을 하였다
화면마다 각자의 역할을 나누었다


### [03/30]

졸업작품 소개 사이트 틀을 제작하였고 전체적인 계획 수립하였다
### [03/23]

기획서 작성 


