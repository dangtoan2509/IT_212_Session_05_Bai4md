## Bài 4 — Phân tích & Lựa chọn (Spring AOP)

- **Lựa chọn:** B

- **Lý do chọn:** Phương án B yêu cầu giải thích theo 2 cấp độ (dễ hiểu và nâng cao), so sánh AOP vs OOP và cung cấp ví dụ thực tiễn ngắn gọn. Cách này giúp người mới hiểu bản chất rồi xem ví dụ thực tế để áp dụng.

- **Nhược điểm phương án B:** Nội dung dài hơn, nhưng đổi lại người học nắm sâu hơn. Các phương án còn lại:
  - A: Quá ngắn, chỉ giải thích + ví dụ nhưng không phân cấp độ học.
  - C: Yêu cầu code và cấu hình pom.xml nhưng thiếu phần giải thích và so sánh khiến người mới khó hiểu bản chất.

- **Ví dụ Aspect (Java Spring Boot) — ghi log thời gian thực thi:**

```java
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.springframework.stereotype.Component;
import lombok.extern.slf4j.Slf4j;

@Aspect
@Component
@Slf4j
public class ExecutionTimeAspect {
    @Around("within(@org.springframework.stereotype.Service *)")
    public Object logExecutionTime(ProceedingJoinPoint pjp) throws Throwable {
        long start = System.currentTimeMillis();
        try {
            return pjp.proceed();
        } finally {
            long duration = System.currentTimeMillis() - start;
            log.info("{} executed in {} ms", pjp.getSignature(), duration);
        }
    }
}
```

