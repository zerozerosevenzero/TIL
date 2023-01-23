파일 원격으로 보내는 명령어
```
scp [OPTION] [user@]SRC_HOST:]file1 [user@]DEST_HOST:]file2
```

## 일반적인 상황
```
scp file.txt remote_username@1.1.1.1:/remote/directory
```

## 파일명을 다르게 저장
```
scp file.txt remote_username@1.1.1.1:/remote/directory/NEW_FILE_NAME.txt
```

## 특정포트로 전송
```
scp -P 1234 file.txt remote_username@1.1.1.1:/remote/directory
```

## 디렉토리 복사 & 전송
```
scp -r /local/directory remote_username@1.1.1.1:/remote/directory
```

