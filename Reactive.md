
blocking model은 많은 thread가 필요하다.

reactive model은 thread가 blocking되지 않는다고 생각한다.   
그래서 event loop용 thread와 core당 1개 정도의 작은 thread pool로 처리한다.

