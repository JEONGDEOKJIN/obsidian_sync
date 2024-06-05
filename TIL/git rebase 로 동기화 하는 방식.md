- develop 브랜치에 있는걸 pull 받아 최신화 시키고 → feature/profile push 하기
    
    1. `feature/profile` 에서 `commit` 함
    2. `develop` 브랜치로 이동 → `git pull origin develop` 해서 원격 develop 과 로컬을 동일하게 만듦
    3. `feature/profile` 브랜치로 이동 → `git rebase develop` → `git push orign feature/profile`
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/97f9c450-95eb-40b2-9139-3ceb6cd26d8c/Untitled.png)
    
- feature/profile 완료되면 → git flow 가서 → gui 로 `merge request` 하는데, `main` 말고, `develop` 으로 가게 해야 함 ⭐⭐⭐⭐⭐⭐ → 그 다음 `delete` 하는 거는 체크 해제!!! 해야 함 ⭐⭐⭐⭐⭐
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/e7e546af-09e1-4aff-81ab-653d08f201b1/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/50fa74f3-a107-45f3-8a1e-d98c0542dd2b/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/33be085c-f344-4b2c-ab5b-b1ff77ea7041/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/4fb4dbc5-25bb-42e8-b588-d24c9c150dc1/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/961a6674-92fa-45c5-98e5-d2a5966ebb5c/Untitled.png)
    
- 그러면 이렇게 됨
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/1577af14-dcb0-45dc-ba49-b0480d60c730/Untitled.png)
    
- develop 에서 main 으로 합치는 건, 하루 마무리 할 때, 선재님이 하실 예정