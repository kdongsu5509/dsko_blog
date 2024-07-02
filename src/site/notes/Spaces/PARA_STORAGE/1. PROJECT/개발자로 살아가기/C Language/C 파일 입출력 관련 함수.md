---
{"dg-publish":true,"permalink":"/spaces/para-storage/1-project//c-language/c/","tags":["C_language","gardenEntry"]}
---

1. **fopen()**: 파일을 열 때 사용되는 함수로, 파일의 경로 및 이름과 열기 모드를 지정합니다.
   ```c
   FILE *fopen(const char *filename, const char *mode);
   ```
   - `filename`: 열고자 하는 파일의 경로 및 이름을 나타내는 문자열.
   - `mode`: 파일을 어떤 형식으로 열지를 지정하는 문자열. 예를 들어, "r"은 읽기 모드, "w"는 쓰기 모드 등이 있습니다.
   - **반환값**: 파일을 성공적으로 열면 `FILE` 포인터를 반환하고, 실패하면 `NULL`을 반환합니다.


2. **fclose()**: 파일을 닫을 때 사용되는 함수입니다.
   ```c
   int fclose(FILE *stream);
   ```
   - `stream`: 닫을 파일을 가리키는 FILE 포인터.
   - **반환값**: 성공하면 0, 실패하면 `EOF`를 반환합니다.


3. **fread()**: 파일에서 데이터를 읽을 때 사용되는 함수입니다.
   ```c
   size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream);
   ```
   - `ptr`: 읽은 데이터를 저장할 버퍼의 포인터.
   - `size`: 각 요소의 크기.
   - `nmemb`: 읽을 요소의 개수.
   - `stream`: 파일 포인터.
   - **반환값**: 실제로 읽은 요소의 개수를 반환합니다.


4. **fwrite()**: 파일에 데이터를 쓸 때 사용되는 함수입니다.
   ```c
   size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *stream);
   ```
   - `ptr`: 쓸 데이터가 저장된 버퍼의 포인터.
   - `size`: 각 요소의 크기.
   - `nmemb`: 쓸 요소의 개수.
   - `stream`: 파일 포인터.
   - **반환값**: 실제로 쓴 요소의 개수를 반환합니다.


5. **fgetc()**: 파일로부터 한 문자를 읽을 때 사용되는 함수입니다.
   ```c
   int fgetc(FILE *stream);
   ```
   - `stream`: 파일 포인터.
   - **반환값**: 읽은 문자 또는 `EOF` (파일의 끝)를 반환합니다.


6. **fputc()**: 파일에 한 문자를 쓸 때 사용되는 함수입니다.
   ```c
   int fputc(int c, FILE *stream);
   ```
   - `c`: 쓸 문자.
   - `stream`: 파일 포인터.
   - **반환값**: 성공하면 쓴 문자를 반환하고, 실패하면 `EOF`를 반환합니다.


7. **fprintf()**: 형식화된 출력을 파일에 쓸 때 사용되는 함수입니다.
   ```c
   int fprintf(FILE *stream, const char *format, ...);
   ```
   - `stream`: 파일 포인터.
   - `format`: 출력 형식을 지정하는 서식 문자열.
   - **반환값**: 성공하면 쓴 문자의 수를 반환하고, 실패하면 `EOF`를 반환합니다.


8. **fscanf()**: 파일로부터 형식화된 입력을 읽을 때 사용되는 함수입니다.
   ```c
   int fscanf(FILE *stream, const char *format, ...);
   ```
   - `stream`: 파일 포인터.
   - `format`: 입력 형식을 지정하는 서식 문자열.
   - **반환값**: 성공하면 읽은 변수의 개수를 반환하고, 실패하면 `EOF`를 반환합니다.


9. **fgets()**: 파일로부터 문자열을 읽을 때 사용되는 함수입니다.
   ```c
   char *fgets(char *str, int n, FILE *stream);
   ```
   - `str`: 읽은 문자열을 저장할 버퍼의 포인터.
   - `n`: 읽을 최대 문자 수.
   - `stream`: 파일 포인터.
   - **반환값**: 성공하면 읽은 문자열을 가리키는 포인터를 반환하고, 실패하면 `NULL`을 반환합니다.


10. **fputs()**: 파일에 문자열을 쓸 때 사용되는 함수입니다.
    ```c
    int fputs(const char *str, FILE *stream);
    ```
    - `str`: 쓸 문자열.
    - `stream`: 파일 포인터.
    - **반환값**: 성공하면 0, 실패하면 `EOF`를 반환합니다.


11. `fseek` 함수는 파일에서의 위치를 이동시킬 때 사용 함수

```c
int fseek(FILE *stream, long int offset, int origin);
```
	- `stream`: 파일 포인터입니다.
	- `offset`: 이동할 바이트 수 또는 이동할 위치를 나타내는 값입니다.
	- `origin`: 파일 포인터의 이동 기준을 지정하는데 사용됩니다. 다음의 값 중 하나일 수 있습니다:
	  - `SEEK_SET`: 파일의 시작부터 `offset` 바이트만큼 이동합니다.
	  - `SEEK_CUR`: 현재 파일 포인터 위치에서 `offset` 바이트만큼 이동합니다.
	  - `SEEK_END`: 파일의 끝에서 `offset` 바이트만큼 이동합니다.

	- **반환값**: 함수가 성공하면 0을 반환합니다. 실패하면 `EOF`를 반환합니다. 주로 `fseek` 함수는 파일의 끝으로 이동하려고 할 때, 또는 에러가 발생했을 때 `EOF`를 반환합니다.