**my project**

팀원 : 홍길동 : 리더 

​           김철수: 코더

### 테스트 **이전 버전으로 돌아가기**

- Reset : 현재 버전을 지우고 이전 버전으로 돌아가기
- Revert : 현재 버전을 그대로 두고 이전 버전으로 돌아가는 commit을 새로 생성
  - 돌아가는 액션도 기록으로 남겨둘 필요가 있을 때
  - 지금까지의 변화는 살리되 특정 버전에서의 작업만 수정이 필요할 때
  - 특히 협업 시에는 공유된 커밋을 삭제하는 것이 매우 크리티컬하다

```cmd
## Reset
# 되돌아갈 시점의 커밋 해시 복사
git reset --hard (돌아갈 커밋 해시)

# 백업한 git 파일로 reset 이전으로 돌아가는 경우 git은 여전히 reset이 적용된 상태를 인식한다
# 현재 커밋 상태로 초기화. 현재는 없지만 reset하면서 다시 생성된 파일은 수동으로 삭제해준다
git reset --hard


## Revert
# 수정할 커밋의 해시를 찾는다
git revert (수정할 커밋 해시)
:wq

# 커밋 수정 내용이 이후 커밋의 코드에 영향을 주는 경우 conflict가 발생하게 된다
# "Replace Lions with Leopards" 커밋을 revert하면 이후 leopard를 수정하는 부분에서 conflict
git revert 6909f6ca6ab597a8b78cfcfc99ee8ca6a85a539a

# 커밋 revert로 삭제가 필요한 leopards.yaml 삭제
git rm leopards.yaml
git revert --continue
:wq

# revert 시에는 commit이 동시에 되는데 commit 없이 revert 하고 싶을 때 
# (다른 액션도 함께 커밋하고 싶을 때)
git revert --no-commit (수정할 커밋 해시)

# 커밋되지 않은 것들을 지우고 현재 커밋 상태로 초기화하고 싶을 때
git reset --hard
```

------

### **Branch** 

#### **Branch는 왜 필요한가?**

- Branch는 분기된 차원으로 프로젝트를 하나 이상의 모습으로 관리해야 할 때
  (실배포용, 테스트 서버용, 새로운 시도용 등)
- 여러 작업들이 각각 독립되어 진행될 때 각각의 차원에서 작업한 뒤 확정된 것을 메인 브랜치에 통합한다

 

#### **Branch 생성/ 이동/ 삭제**