# 안드로이드 클린 아키텍처

Created: 2023년 4월 9일 오후 5:10

- 클린 아키텍처
    <img src="%E1%84%8B%E1%85%A1%E1%86%AB%E1%84%83%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%20%E1%84%8F%E1%85%B3%E1%86%AF%E1%84%85%E1%85%B5%E1%86%AB%20%E1%84%8B%E1%85%A1%E1%84%8F%E1%85%B5%E1%84%90%E1%85%A6%E1%86%A8%E1%84%8E%E1%85%A5%20cfe762c241694d20b93e6e88a54a66e0/Untitled.png" width="350" height="250">
    
    - 외부 인터페이스에서 독립적으로 구현
    - 의존성 : 바깥쪽 원 → 안쪽 원
    ⇒ 바깥쪽 원은 안쪽 원에 영향을 주지 않는다!
    - 목표 : 바깥 레이어가 정해지지 않아도 서비스를 구축할 수 있도록

- 각 계층 설명
    - Entities
        - 핵심 비즈니스 규칙을 캡슐화
        - 메소드를 가지는 객체
        - 데이터 구조와 함수의 집합
        - 가장 안쪽의 객체 ⇒ 외부로부터 영향을 받지 않음
    - Use Cases
        - 어플리케이션 고유 비즈니스 규칙 포함
        - Entity 로 들어가고 나오는 데이터 흐름을 조합
        - ex) 상품 목록오는 기능 : 목록을 읽어오기 위한 로직
    
    - Interface Adapter
        - Entity 와 Use Cases 의 데이터를 외부 계층에 적용할 수 있는 형식으로 변환
        - ex) MVC - Controller, MVP - Presenter, MVVM - ViewModel
    
    - Framework & Driver
        - 시스템의 핵심 업무와는 관련 X
        - 네크워크, DB …
    
- 안드로이드 클린 아키텍처
    
    <img src="%E1%84%8B%E1%85%A1%E1%86%AB%E1%84%83%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%20%E1%84%8F%E1%85%B3%E1%86%AF%E1%84%85%E1%85%B5%E1%86%AB%20%E1%84%8B%E1%85%A1%E1%84%8F%E1%85%B5%E1%84%90%E1%85%A6%E1%86%A8%E1%84%8E%E1%85%A5%20cfe762c241694d20b93e6e88a54a66e0/Untitled%201.png" width="200" height="200">
    
    <img src="%E1%84%8B%E1%85%A1%E1%86%AB%E1%84%83%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%20%E1%84%8F%E1%85%B3%E1%86%AF%E1%84%85%E1%85%B5%E1%86%AB%20%E1%84%8B%E1%85%A1%E1%84%8F%E1%85%B5%E1%84%90%E1%85%A6%E1%86%A8%E1%84%8E%E1%85%A5%20cfe762c241694d20b93e6e88a54a66e0/Untitled%202.png" width="500" height="400">
    
    <img src="%E1%84%8B%E1%85%A1%E1%86%AB%E1%84%83%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%20%E1%84%8F%E1%85%B3%E1%86%AF%E1%84%85%E1%85%B5%E1%86%AB%20%E1%84%8B%E1%85%A1%E1%84%8F%E1%85%B5%E1%84%90%E1%85%A6%E1%86%A8%E1%84%8E%E1%85%A5%20cfe762c241694d20b93e6e88a54a66e0/Untitled%203.png" width="300" height="200">
    

- 프레젠테이션 계층 (Presentation Layer)
    - UI 와 관련된 계층
    - **Domain 계층에 의존성**을 갖는다.
    - 의존성 방향 : Presentation → Domain ←Data
    - 뷰 (View)
        - UI 화면 표시와 사용자 입력
        - 프레젠터가 명령하는 일만 수행
        - **Activity, Fragment**
    - 프레젠터 (Presenter)
        - 사용자 입력이 왔을 때 어떤 반응을 해야 하는지에 대한 판단을 한는 영역
        - UI 업데이트와 관련된 로직 구현
        - **ViewModel**
        
- 도메인 계층 (Domain Layer)
    - 비즈니스 로직 처리
    - **Repository 인터페이스** 포함
    
    - 유즈 케이스 (Use Case)
        - 각 개별 기능 or 비즈니스 논리 단위
        - 서비스를 사용하고 있는 사용자가 해당 서비스를 통해 하고자 하는 것
    
    - 모델 (Model)
        - Domain 계층에서 사용되는 데이터 모델
        - 앱의 실질적 데이터
        - 네트워크 통신이나 로컬 DB 로 받은 데이터를 가공한 데이터
        
    - 단순한 mapper 가 아닌 경우에는 도메인 계층에 들어갈 수도 있다!
        - translating 하거나 암호화 하거나
        - 세부적으로 더 mapping 이 필요한 경우
        - mapping 하는 것도 비즈니스 로직일 수도 있기 때문에!
    
    ![Untitled](%E1%84%8B%E1%85%A1%E1%86%AB%E1%84%83%E1%85%B3%E1%84%85%E1%85%A9%E1%84%8B%E1%85%B5%E1%84%83%E1%85%B3%20%E1%84%8F%E1%85%B3%E1%86%AF%E1%84%85%E1%85%B5%E1%86%AB%20%E1%84%8B%E1%85%A1%E1%84%8F%E1%85%B5%E1%84%90%E1%85%A6%E1%86%A8%E1%84%8E%E1%85%A5%20cfe762c241694d20b93e6e88a54a66e0/Untitled%204.png)
    

- 데이터 계층 (Data Layer)
    - 데이터를 컨트롤하는 계층
    - **Domain 계층에 의존성**을 갖는다.
    - **Repository 구현**
    
    - 리포지토리 (Repository)
        - 유즈 케이스가 필요로 하는 데이터를 저장, 수정
        - 데이터 소스를 인터페이스로 참조 ⇒ 로컬 DB 와 네트워크 통신 수행
        
    - 데이터 소스 (Data Source)
        - 실제 데이터의 입출력 수행하는 부분

- 예시
    - Domain 계층
        - Repository 인터페이스
            - Product 리스트 가져오기 위한 Repository 의 인터페이스 생성
            - Repository 구현체는 Data 계층에 속함
                
                ```kotlin
                interface ProductRepository {
                   suspend fun getProductList(): Flow<NetworkResult<ProductList>>
                }
                ```
                
        - UseCase
            - Product 목록을 가져오는 기능을 제공하는 유스케이스
            - 위에서 선언한 Repository 인터페이스를 생성자로 주입
            - 데이터를 가져오는 역할
            - 이름만 보고도 어떤 기능을 하는지 알아야함
                
                ```kotlin
                class GetProductUseCase @Inject constructor(private val productRepository : ProductRepository ) : BaseApiResponse() {
                   suspend fun invoke(): Flow<NetworkResult<ProductList>> = productRepository.getProduct()
                }
                ```
                
        - Model
            - Data 클래스로 생성해도 되지만, Data 계층에서 mapper 를 통한 변환 ⇒ 별도의 연산 필요할 수 있다!
            - Domain 계층에서 interface 로 생성하고 Data 계층에서 구현하는 방식으로 설계하자!
            - Domain 계층에서의 Data Model 과 Data 계층에서의 Data Model 은 **같을 수 있다.**
                - 서버 api 에서 가져온 데이터를 모두 사용하는 경우 → 같음
                - 두 Data Model 이 다른 경우 → Data 계층에서 Domain 계층으로 필요한 데이터만 추출해서 넘겨준다면, 서로 다르다.
                
                ex) 서버에서 Github Repository 정보 가져오는 예시
                
                - Domain 계층의 Model
                
                ```kotlin
                interface GithubRepo {
                    val name: String
                    val url: String
                }
                ```
                
                - Data 계층의 Model
                
                ```kotlin
                data class GithubRepoRes(
                    @SerializedName("name")
                    private val _name: String,
                
                    @SerializedName("id")
                    private val _id: String,
                
                    @SerializedName("created_at")
                    private val _date: String,
                
                    @SerializedName("html_url")
                    private val _url: String
                ) : GithubRepo {
                    override val name: String
                        get() = _name
                
                    override val url: String
                        get() = _url
                }
                ```
                
    - Data 계층
        - Data Model
            - api 호출을 통해 데이터를 가져올 모델
                
                ```kotlin
                	data class Product(
                   @SerializedName("id") val id: Int,
                   @SerializedName("title") val title: String,
                   @SerializedName("description") val description: String,
                   @SerializedName("price") val price: Int,
                   @SerializedName("discountPercentage") val discount: Double,
                   @SerializedName("rating") val rating: Double,
                   @SerializedName("stock") val stock: Int,
                   @SerializedName("brand") val brand: String,
                   @SerializedName("category") val category: String,
                   @SerializedName("thumbnail") val thumbnail: String,
                   @SerializedName("images") val imageList: Array<String>,
                ) : java.io.Serializableapi service
                ```
                
        - Repository 구현체
            
            ```kotlin
            
            class ProductRepositoryImpl @Inject constructor(
            	private val productApi: ProductApi
            ) : ProductRepository {
               fun getProductList(): Flow<NetworkResult<ProductList>> {
                  return flow {
                     emit(safeApiCall { productApi.getProductList() })
                  }.flowOn(Dispatchers.IO)
               }
            }
            ```
            
            구현체가 필요한 이유?
            
            의존성 역전! 
            객체지향의 원칙인 solid 를 지키기 위해
            
    - Presentation 계층
        - ViewModel
            
            ```kotlin
            @HiltViewModel class MainViewModel @Inject constructor(
               private val getProductUseCase: GetProductUseCase,
            ) : ViewModel() {
               private val _response: MutableLiveData<NetworkResult<ProductList>> = MutableLiveData()
               val response: LiveData<NetworkResult<ProductList>> = _response
            
               fun getProductList() = viewModelScope.launch {
                  getProductUseCase.invoke().collect { values ->
                     _response.value = values
                  }
               }
            }
            ```
            
        - Fragment
            
            ```kotlin
            viewModel.getProductList()
                  viewModel.response.observe(viewLifecycleOwner) { response ->
                     when (response) {
                        is NetworkResult.Success -> {
                           Log.w("Network ", "Success")
                           productListAdapter.submitList(response.data?.list)
                        }
            
                        is NetworkResult.Error -> {
                           Log.e("Network Error", response.message.toString())
                        }
            
                        is NetworkResult.Loading -> {
                           Log.w("Network ", "Loading")
                        }
                     }
                  }
            ```
            
        - 참고:
            
            [https://velog.io/@im_ssu/안드로이드에-클린아키텍처-적용하기](https://velog.io/@im_ssu/%EC%95%88%EB%93%9C%EB%A1%9C%EC%9D%B4%EB%93%9C%EC%97%90-%ED%81%B4%EB%A6%B0%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0)
            [https://velog.io/@galaxy/Clean-Architecture#domain-1](https://velog.io/@galaxy/Clean-Architecture#domain-1)
            [https://leveloper.tistory.com/205](https://leveloper.tistory.com/205)
            
    다음주 숙제! 함수형 프로그래밍이 뭔지, 함수형 클린 아키텍처가 어떻게 사용되는지?