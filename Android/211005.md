# Recycleview 와 Listview
>Recyclerview : 사용자가 관리하는 많은 수의 데이터 집합을 개별 아이템 단위로 구성하여
화면에 출력하는 뷰그룹

>Listview : 데이터 목록이 화면을 넘어가면 스크롤 할 수 있게 해주는, 데이터 목록을 화면에 출력하는 뷰

# 차이점

## ViewHolder
- Recyclerview : 뷰홀더 패턴을 이용함
- Listview : 뷰홀더 패턴을 이용하지 않음 


## Item Layout
- Recyclerview : 가로,세로,grid 형식 모두 지원
- Listview : 세로 방향만 지원

## Item Animation
- Recyclerview : 아이템 애니메이셔 처리 클래스 존재
- Listview :아이템 추가/제거시에 적용가능한 애니메이션 없음

## Decoration
- Recyclerview : RecyclerView.ItemDecoration 객체를 사용하여 구분선을 설정해야함
- Listview : Android:divider 속성을 이용하여 리스트에 있는 아이템을 쉽게 구분할 수 있음



---
# 결론
> Recyclerview 는 Listview에 유연함과 성능을 더한것 (Recyclerview > Listview)
