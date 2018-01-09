单个case的yaml定义
```yaml
metadata: 
   name: #case名称,可自行修改
   format: #目前是lava definition 1.0 
   description: #对case的简单描述
   maintainer: #维护此case的作者邮箱
   scope: #case所属类别
   os: #支持的操作系统(发行版)
   devices: #支持的设备(开发板)
   level: #优先级设置（值为1到5,1为最高，5为最低）
install:
   deps: #所需的安装包(所有系统共用)
params:
   #所需参数
run:
   steps:安装之后的动作(终端命令)
   #例如: - "cd app/ftp; ./ftp.sh; cd -"
parse:
   #解析case测试结果,按如下方式书写即可:
   pattern: "^(?!.+ED)(?P<test_case_id>\\w+)\\s+(?P<result>\\w+)\\s+\\d$"
   fixupdict:
      FAIL: fail
      PASS: pass
```

test plan中的yaml定义
```yaml
metadata:
  # name key is needed by test-runner
  name: linux-test-plan-example
  description: Linux test plan example
  os: debian
  devices:
    - d05
    - hi6220-hikey
    - dragonboard410c
  maintainer:
    - first.last@linaro.org
  approver:
    - first.last@linaro.org
  owner:
    - first.last@linaro.org
  # format key is needed by test-runner
  format: Linaro Test Plan v2

tests:
  automated:
    - path: automated/linux/smoke/smoke.yaml
      repository: https://git.linaro.org/qa/test-definitions.git
      timeout: 900
    - path: automated/linux/toolchain-smoke/toolchain-smoke.yaml
      repository: https://git.linaro.org/qa/test-definitions.git
      parameters:
	SKIP_INSTALL: True
	STATIC: True
      timeout: 900
  manual:
    - path: manual/generic/linux/disk-boot.yaml
      repository: https://git.linaro.org/qa/test-definitions.git
    - path: manual/generic/serial-console.yaml
      repository: https://git.linaro.org/qa/test-definitions.git
```