[페이즈1]
execve의 환경 변수로 /usr/bin 과 /bin을 주어 이 내부의 명령어들을 사용할 수 있도록 설정했습니다.
myshell을 실행한 후 ls,pwd,echo,touch,cat,ps 등을 사용할 수 있습니다.
따옴표 설정을 수행했고, 페이즈1의 빌트인 명령어로는 cd를 두어 cd 명령어를 사용할 수 있도록 했습니다.
SIGINT와 SIGTSTP의 시그널을 무시하여 해당 CTRL+Z, CTRL+C를 사용할 수 없습니다.
-----------------------------------------------------------------------------------------------------------------
[페이즈2]
페이즈1에서 사용 가능하도록 만든 명령어를 적절히 조합하여 파이프를 사용할 수 있습니다.
pipe()와 dup2() 함수를 재귀 함수를 통해 구현하였습니다.
ex) ls -al | grep myshell | sort -r | wc -l
----------------------------------------------------------------------------------------------------------------
[페이즈3]
페이즈 2에 더해 각종 프로세스를 &를 사용해 백그라운드로 돌리거나, 백그라운드를 포어그라운드로 전환하거나,
CTRL+C CTRL+Z를 통해 포어그라운드 프로세스를 종료 또는 정지하는 등의 명령이 가능합니다.
jobs,kill,fg,bg의 빌트인 명령어가 추가되었습니다.

표준 입력으로 입력한 프로세스를 백그라운드로 돌리기 시작하면 ps를 입력했을때 myshell 프로세스가 여러개 발견되는데, 이는 각 백그라운드 프로세스들이
종료되기를 wait하고 있는 waiting process들이며, 자식 프로세스가 종료되며 함께 종료됩니다.