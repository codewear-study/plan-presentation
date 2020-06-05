스마트 포인터는 객체에 유효한 스코프가 더 이상 없을 때 자동으로 메모리를 해제한다.

C++14이상에서는 절대 일반포인터에 메모리 할당을 하지 말라고 한다. 대신 항상 스마트 포인터를 쓰도록 한다.

<memory> 헤더 파일에 정의되어있다.

스마트 포인터는 포인터의 역할을 할 수 있지만 포인터가 아닌 하나의 객체이다. 대신 포인터가 하는 기능들을 오버로딩해 놓아서 포인터의 역할을 할 수 있는 것이다.

- std::unique_ptr

  보통의 포인터랑 비슷하지만 스코프를 벗어날때 자동으로 메모리를 해제하며, 명시적으로 delete를 통해 해제될 수 있다.

  유니크 하다는 이름과 같이 해당 객체를 참조하는 스마트 포인터는 오직 하나만 존재하는 것을 보장한다.  이를 통해 예외 상황이 발생했을 때 메모리 해제를 단순하게 할 수 있다.

  ```cpp
  class Bee {
  private:
  	int a;
  	int b;
  
  public:
  	Bee() {
  		this->a = 0;
  		this->b = 0;
  	}
  	Bee(int a, int b) {
  		this->a = a;
  		this->b = b;
  	}
  	int get_a() {
  		return a;
  	}
  	int get_b() {
  		return b;
  	}
  };
  
  int main(){
  //C++14이전:bee1이라는 유니크 포인터를 만들면서 그에 대한 파라미터로 가리킬 객체를 생성
  	std::unique_ptr<Bee> bee1(new Bee);
  	std::unique_ptr<Bee> bee2(new Bee(1, 2));
  //C++14부터는 make_unique()라는 것이 생겼다.
  	std::unique_ptr<Bee> bee3 = std::make_unique<Bee>();
  	std::unique_ptr<Bee> bee4 = std::make_unique<Bee>(1, 2);
  	auto bee5 = std::make_unique<Bee>(); //이것도 가능
  
  //같은 unique_ptr들이 같은 곳을 가리키는 것을 막는다.
  	auto be1 = std::make_unique<Bee>(); //가능
  	std::unique_ptr<Bee> be2(be1); //불가능
  	std::unique_ptr<Bee> be3(be1); //불가능
  
  	return 0;
  }
  ```

  억지로 각 unique_ptr이 가리키는 것이 같게 만들 수는 있다. 하지만 unique_ptr은 스코프밖으로 벗어나는 순간 가리키고 있던 객체를 메모리에서 해제해버린다. 그래서 다른 포인터들이 이미 사라져 버린 객체를 가리키고 있을 수도 있게 된다.

  ```cpp
  Bee* bee1 = new Bee(1, 2);
  std::unique_ptr<Bee> bee2(bee1);
  std::unique_ptr<Bee> bee3(bee1);
  ```

  그래서 위와 같이 같은 것을 가리키는 것을 막기 위해 make_unique()는 무조건 새로운 객체를 만들어 저장하도록 되어있다.

  ### move()

  ```cpp
  auto u_ptr = std::make_unique<Bee>(1, 2);
  auto u_ptr2 = move(u_ptr);
  ```

  또는 위와 같이 move()를 통해 완전히 오너십을 넘겨야 한다. 그러면 u_ptr이 가리키던 것을 u_ptr2가 가리키게 되고 u_ptr은 더 이상 사용할 수 없게 된다.

  ### get()

  ```cpp
  auto u_ptr = std::make_unique<Bee>(3, 5);
  Bee* b = u_ptr.get();
  ```

  내부에 저장된 포인터를 반환한다. 이 경우 오너십을 넘기지 않는다.

  ### reset()

  ```cpp
  auto u_ptr = std::make_unique<Bee>(1, 2);
  u_ptr.reset();
  u_ptr.reset(new Bee(3, 5));
  ```

  내부에 있는 저장된 포인터가 가리키는 객체를 해제하고 저장된 포인터는 nullptr로 변경하거나 새로운 메모리 할당이 가능하다.

  ### release()

  ```cpp
  auto u_ptr = std::make_unique<Bee>(1, 2);
  Bee* b = u_ptr.release();
  ```

  내부에 저장된 포인터를 반환하고 nullptr로 변경한다.  포인터가 가리키는 메모리를 해제하지 않기 때문에 사용자가 해제해주어야 한다.

  unique_ptr은 다른 스마트 포인터와 다르게 아래와 같이 배열도 가능하지만 std::array나 std::vector와 같은 STL컨테이너를 이용하는 것이 바람직하다.

  ```cpp
  auto u_ptr = make_unique<int[]>(10); //크기가 10인 int형 배열
  auto u_ptr2 = make_unique<vector<int>>(); //벡터 컨테이너
  auto u_ptr3 = make_unique<array<int, 10>>(); //어레이 컨테이너
  ```