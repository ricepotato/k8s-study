# k8s study

https://github.com/sysnet4admin/_Book_k8sInfra/

## kubectl

### 연결된 노드 확인

```bash
kubectl get nodes
```

### pod 확인

```bash
kubectl get pods -o wide
kubectl get pods -o=custom-columns=NAME:.metadata.name,IP:.status.podIP,STATUS:.status.phase,NODE:.spec.nodeName
kubectl get pod [pod 이름] -o yaml > pod.yaml # pod 상세 정보 yaml 파일로 출력
```

### pod 생성

pod 생성 명령어 kubectl run

```bash
kubectl run nginx-pod --image=nginx
```

pod 생셩 명령어 kubectl create

kubectl create 는 deployment 를 추가해서 생성해야 한다.

```bash
kubectl create deployment dpy-nginx --image=nginx
```

### pod 삭제

```bash
kubectl delete pods [pod 이름]
```

### deployment 생성과 삭제 명령어

```bash
kubectl create deployment dpy-hname --image=sysnet4admin/echo-hname
kubectl delete deployment dpy-hname
```

### deployment scale

dpy-nginx deployent 를 3개로 scale

```bash
kubectl scale deployment dpy-nginx --replicas=3
```

### yaml 파일을 이용하여 object 생성

```bash
kubectl create -f [파일명.yaml]
```

### object 를 삭제하지 않고 변경사항 적용

```bash
kubectl apply -f [파일명.yaml]
```

### deployment pod 업데이트 record

```bash
kubectl apply -f ~/_Book_k8sInfra/ch3/3.2.10/rollout-nginx.yaml  --record
```

### deployment rollout history

```bash
kubectl rollout history deployment [deployment 이름]
```

### deployment rollout status

```bash
kubectl rollout status deployment [deployment 이름]
```

### deployment set image

```bash
kubectl set image deployment rollout-nginx nginx=nginx:1.16.0 --record
```

### deployment 상태 보기

```bash
kubectl describe deployment [deployment 이름]
```

### rollout undo

```bash
kubectl rollout undo deployment [deployment 이름]
```

### 특정 revision 으로 돌아가기

```bash
kubectl rollout undo deployment [deployment 이름] --to-revision=1
```

### 사용가능한 api verion 확인

```bash
kubectl api-version
```

### cordon/uncordon 명령으로 특정노드에 schedule 되지 않게 하기

```bash
kubectl cordon w3-k8s
kubectl uncordon w3-k8s
```

### drain 명령으로 특정노드의 pod 를 다른 node 로 이동

```bash
kubectl drain w3-k8s --ignore-daemonsets
```

다시 node 에 pod 를 할당하려면 uncordon 실행

```bash
kubectl uncordon w3-k8s
```

### kubernates 구성요소 확인

```bash
kubectl get pods --all-namespaces
```

### kubernates service

#### node port

모든 워커 노드의 특정 포트를 열고 여기로 들어오는 모든 요청을 노트포트 서비스로 전달

kubectl expose 는 port 를 지정할 수 없음.

```bash
kubectl expose deployment np-pods --type=NodePort --name=np-svc-v2 --port=80
```

## vagrant

초기화

```bash
vagrant init
```

Vagrantfile 생성됨

```bash
vagrant ssh
```

vagrant 로 생성된 가상머신에 ssh 접근

머신 삭제

```bash
vagrant destroy -f
```

machine 삭제, 강제종료
