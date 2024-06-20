AWS CloudFormation 템플릿을 사용하여 API 요청을 처리하는 Lambda 함수와 클라이언트 ID를 저장하는 DynamoDB 테이블을 생성합니다. 
그런 다음 API Gateway 콘솔을 사용하여 Lambda 함수와 통합되는 WebSocket API를 생성합니다.
마지막으로 API를 테스트하여 메시지가 전송되고 수신되는지 확인한다.


웹소켓을 통해 연결, 메시지 전송, 연결 해제를 처리하는 Lambda 함수와 DynamoDB 테이블, IAM 역할과 정책을 정의한다.

DynamoDB 테이블 생성
 -ConnectionsTable8000B8A1: connectionId라는 키를 사용하여 연결 정보를 저장하는 테이블을 만듭니다.
IAM 역할 및 정책 생성
ConnectHandlerServiceRole7E4A9B1F,
DisconnectHandlerServiceRoleE54F14F9,
SendMessageHandlerServiceRole5F523417, 
DefaultHandlerServiceRoleDF00569C
- 각 Lambda 함수가 필요한 권한을 가지도록 IAM 역할을 만듭니다. 각 역할에는 Lambda 함수가 DynamoDB 테이블에 읽기, 쓰기, 업데이트, 삭제 등의 작업을 수행할 수 있도록 정책을 연결.

Lambda 함수 생성
ConnectHandler2FFD52D8: 사용자가 웹소켓에 연결할 때 호출되는 함수입니다. 연결 정보를 DynamoDB 테이블에 저장합니다.
DisconnectHandlerCB7ED6F7: 사용자가 웹소켓에서 연결을 끊을 때 호출되는 함수입니다. 연결 정보를 DynamoDB 테이블에서 삭제합니다.
SendMessageHandlerDCEABF13: 사용자가 메시지를 보낼 때 호출되는 함수입니다. 연결된 모든 사용자에게 메시지를 전달합니다.
DefaultHandler604DF7AC: 기본 경로로 요청이 들어올 때 호출되는 함수입니다. 사용자가 메시지를 어떻게 보낼 수 있는지 안내 메시지를 보냅니다.


정책 연결
각 Lambda 함수와 IAM 역할이 제대로 작동하도록 정책과 역할을 연결합니다
