# **DiffUtil, ListAdapter**

원래 **RecyclerView** 의 데이터가 변경되면

![image](https://cdn.discordapp.com/attachments/892277737266499614/963769489948807208/unknown.png)

**RecyclerView** **Adapter** 가 제공하는 **NotifyItem** **Method** 를 통해 **ViewHolder** 의 내용을 갱신했다

위의 방식의 문제점은 매번 **Data** 가 변경되는 방식을 확인해야하고 그때마다 하나하나 **Notify** 를

해줘야하며 갱신이 필요없는 **ViewHolder** 도 변경하며 불필요한 작업을 만들어낸다는 것이다

하지만 **DiffUtil** 은 다르다

---

>## **😎 DiffUtil**

<br>

**DiffUtil** 은 두개의 **DataSet** 을 받아서 두개의 차이를 계산해주는 **Class** 이다

**DiffUtil** 을 사용하면 두개의 **DataSet** 을 계산하고 변한부분만 파악해서

**RecyclerView** 에 반영을 할 수 가 있다

이 **DiffUtil** 은 *Eugene W. Myers* 의 **difference** 알고리즘을 이용해서 비교 연산을 완료한다

```
O(N + D^2) // 비교 연산 시간

N: 추가 및 제거된 항목의 갯수
D: 스크립트의 길이
``` 
![image](https://cdn.discordapp.com/attachments/892277737266499614/963772424128712714/unknown.png)

**DiffUtil** 을 사용하기 위해서는 **DiffUtil** 의 **Callback** 을 상속받아서

- *areItemsTheSame()*  **- 비교 대상의 객체가 동일한지 확인**
- *areContentsTheSame()* **- 두개의 item 이 내용까지 동일한 data 를 가지는지 확인**

다음과 같은 **Method** 를 활용한다

---

>## **😎 AsyncListDiffer**

<br>

**DiffUitl** 은 **Item** 은 개수가 많을 경우엔 비교 연산의 시간에
길어지기에 **Background Thread** 에서 처리되어야한다

**AsyncListDiffer** 은 **DiffUtil** 을 쉽게 사용하기 위해 만들어진 **class** 로 **DiffUtil** 에 자체적으로 스레드 처리를 해준다

<br>

![image](https://cdn.discordapp.com/attachments/899472345763295342/964166755763245116/unknown.png)

<br>

**AsyncListDiffer** 을 사용하기 위해서는 **adapter** 내부로 **DiffUt Callback** 을 전달받은

**AsyncListDiffer** 을 만들어줘야한다 이렇게 되면 **mDiffer** 라는 객체를 만든 후에

**currentList()** 로 **Data** 를 참조하고 **submitList()** 로 갱신된 **List** 를 보내주면되는데

**currentList()** 는 기존의 **Data** , **submitList()** 는 새로운 **Data** 로 전달을 하면된다

---

>## **😎 ListAdapter**

<br>

**ListAdater** 은 앞서 말한 **AsyncListDiffer** **Class** 를 더 쓰기 편하게 랩핑한 **Class** 다

<br>

![image](https://cdn.discordapp.com/attachments/899472345763295342/964579503894560778/unknown.png)

<br>

**RecyclerView Adapter** 을 만들때 이 **List Adapter** 을 상속하게 하도록 하면 사용할 수 있다

초기화 할 때 **DiffUtil Callback** 객체를 받도록 하면 나머진 **AsyncListDiffer** 처럼

*currentList()* 로 현재 **List** 를 불러올수있고 *submitList()* 로 **List** 를 갱신할수있다

그래서 *submitList()* 로 전체 **Data** 를 넘겨주면 **Adapter** 가 **Background Thread** 를 이용해

***List*** 의 차이를 계산하고 그에 따라 화면을 갱신시켜준다

<Br>

<br>

**예제는 다음의 링크에서 확인할 수 있다**

-> https://github.com/jongjin1010/DiffUtil













