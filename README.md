# worker_control

worker_control manage go worker in a project, and put worker to group, support start, stop method.

## Usage

```
import (
    workerControl "github.com/rfyiamcool/worker_control"
)

type TimerWorker struct {}

func (t *TimerWorker) Start(){
}

func (t *TimerWorker) Stop(){
}

func (t *TimerWorker) GetProcessName() string {
    return "timer"
}

func main(){
    wm := workerControl.NewWorkerControl()
    timer := TimerWorker{}
    wm.AddWorkerList(timer)

    wm.Start()
    wm.MakeRecvSignal()
    wm.Stop()

    exitCode := wm.WaitTimeout(30) // after 30s, force exit
    switch exitCode {
    case workerControl.ForceTimeoutExitCode:
        tool.Log.Errorf("timeout force exit, timeout: %v", forceExitTime)

    case workerControl.GracefulExitCode:
        tool.Log.Info("graceful exit")
    }
}


```