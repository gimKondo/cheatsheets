# Linux
## PC性能確認
- CPUコア数
	- `nproc`
	- `cat /proc/cpuinfo | grep -c processor`
		- 各プロセッサごとに情報が載っており、processorの出現数がコア数に一致
	- `lscpu`
		- CPU情報が分かりやすく表示される

