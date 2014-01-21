#### [How to operate make -j option](http://stackoverflow.com/questions/2367284/how-does-the-make-j-option-actually-work)

* man page 내의 -j 옵션 설명
 * -j [jobs], -jobs[=jobs]
 * Specifies the number of jobs (commands) to run simultaneously. If there is more than one -j option, the last one is effective. If the -j option is given without an argument, make will not limit the number of jobs that can run simultaneously.

* 핵심 정리
 * target과 prerequisite 관계에 따라 dependency graph 생성 
 * 생성된 dependency graph를 topological sorting 방법으로 순회하며 빌드 순서를 정한다. 
 * 빌드가 되는 대상은 dependency-less target 이므로 -j 옵션에 주어진 개수만큼 동시에 빌드할 수 있다. (물론 물리적으론 CPU 제약이 있겠지만)

* -j 옵션을 사용하지 않는 경우와의 차이점
 * -j 옵션을 사용하면 dependency graph를 topological sort 방식으로 traversal 
 * -j 옵션을 사용하지 않으면 dependency graph를 depth-first, left-to-right search 방식으로 traversal
