- **准备调试环境(支持test-runner)**
```bash
git clone https://git.linaro.org/qa/test-definitions.git
cd test-definitions
. ./automated/bin/setenv.sh
wget https://bootstrap.pypa.io/get-pip.py
python get-pip.py
pip install -r ${REPO_PATH}/automated/utils/requirements.txt
(opensuse: pip2 install -r ${REPO_PATH}/automated/utils/requirements.txt )
cd -
```

- **拷贝lava_test_shell(支持lava返回结果)**
```bash
cd /root
#注意下面使用自己的账户
scp -r liucaili@192.168.1.107:/home/liucaili/lava_test_shell .
chmod 777 -R lava_test_shell
export PATH=/root/lava_test_shell:$PATH
echo $PATH
cd -
```

- **调试用例**
```bash
#1.拷贝测试用例仓库
git clone https://github.com/open-estuary/test-definitions.git
#2.调试单个用例
1)将case对应的yaml中run/step下路径临时修改成:
cd test-definitions/auto-test/*** 
2)test-runner -d test-definitions/auto-test/***.yaml
#2.调试plan
1)将plan对应的yaml中test/automated/path的路径临时修改成:
test-definitions/auto-test/***.yaml
2)将case对应的yaml中run/step下路径临时修改成:
cd test-definitions/auto-test/*** 
3)test-runner -p test-definitions/plans/***.yaml
```