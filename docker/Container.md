[Reference](https://docs.docker.com/get-started/overview/)

## Container 란?
Host OS와 격리되어, 독립적으로 실행 가능한 소프트웨어 단위.   
namespace 가상화를 이용하여 시스템을 격리.

### Namespace
* MNT (Mount)
* IPC (Inter-process-communication)
* PID (process)
* NET (network)
* UTS (hostname)
* UID (user)

### Image
`Container`를 만들기 위한 절차와 파일이 기록되어 있는 read-only template.   

