# presigned url?

S3 파일을 안전하게 공유하고 싶을 때 사용
생성자가 가진 권한으로 파일에 접근 가능한 임시 URL을 생성
 - URL만료기간 지정 가능
 - Http Method 설정 가능
 - URL의 권한은 생정자가 가진 권한 중 일부 혹은 전체 사용

ec2 s3서명 설정 명령어
aws configure set default.s3.addressing_style virtual

ec2 파일 등록
aws s3 presign s3://josun-presigned-url-test/mike.jpg --region ap-northeast-2

파일 만료기간 등록
aws s3 presign s3://josun-presigned-url-test/mike.jpg --region ap-northeast-2 --expires-in 10
