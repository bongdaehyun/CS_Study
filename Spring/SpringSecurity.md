# Spring Security

# ๐ก์คํ๋ง ์ํ๋ฆฌํฐ ๋?

- ์คํ๋ง ๊ธฐ๋ฐ์ ์ ํ๋ฆฌ์ผ์ด์์ ๋ณด์(์ธ์ฆ๊ณผ ๊ถํ, ์ธ๊ฐ ๋ฑ)์ ๋ด๋นํ๋ ์คํ๋ง ํ์ ํ๋ ์ ์ํฌ์๋๋ค. ์ฆ ์ธ์ฆ(Authenticate) ๊ณผ ์ธ๊ฐ(Authorize)๋ฅผ ๋ด๋นํ๋ ํ๋ ์ ์ํฌ
- ์๋ธ๋ฆฟ filter์ ์ด๋ค๋ก ๊ตฌ์ฑ๋ ํํฐ์ฒด์ธ์ผ๋ก์ ๊ตฌ์ฑ๋ ์์๋ชจ๋ธ์ ์ฌ์ฉ
- ๋ณด์๊ณผ ๊ด๋ จํด์ ์ฒด๊ณ์ ์ผ๋ก ๋ง์ ์ต์์ ์ ๊ณตํด์ฃผ๊ธฐ ๋๋ฌธ์ ๊ฐ๋ฐ์ ์์ฅ์์๋ ์ผ**์ผ์ด ๋ณด์๊ด๋ จ ๋ก์ง์ ์์ฑํ์ง ์์๋ ๋๋ค๋  ์ฅ์ **

## ๐์คํ๋ง ์ํ๋ฆฌํฐ ํน์ง๊ณผ ๊ตฌ์กฐ

- ๋ณด์๊ณผ ๊ด๋ จํ์ฌ ์ฒด๊ณ์ ์ผ๋ก ๋ง์ ์ต์์ ์ ๊ณตํ์ฌ ํธ๋ฆฌ
- Filter ๊ธฐ๋ฐ์ผ๋ก ๋์ํ์ฌ MVC์ ๋ถ๋ํ์ฌ ๊ด๋ฆฌ ๋ฐ ๋์
- ์ด๋ธํ์ด์์ ํตํ ๊ฐ๋จํ ์ค์ 
- Spring Security๋ ๊ธฐ๋ณธ์ ์ผ๋ก ์ธ์ & ์ฟ ํค๋ฐฉ์์ผ๋ก ์ธ์ฆ

![image/security.png](image/security.png)

- **์ธ์ฆ๊ด๋ฆฌ์** ์ **์ ๊ทผ ๊ฒฐ์  ๊ด๋ฆฌ์**๋ฅผ ํตํด ์ฌ์ฉ์์ ๋ฆฌ์์ค ์ ๊ทผ์ ๊ด๋ฆฌ
- ์ธ์ฆ ๊ด๋ฆฌ์๋**UsenamePasswordAuthenticationFilter** ์ ๊ทผ ๊ฒฐ์  ๊ด๋ฆฌ์๋**FilterSecurityInterceptor**

## ๐๊ธฐ๋ณธ ๊ตฌ์กฐ

![image/security2.png](image/security2.png)

## โ๏ธํํฐ๋ณ ๊ธฐ๋ฅ ์ค๋ช

- **SecurityContextPersistenceFilter**

SecurityContextRepository์์ SecurityContext๋ฅผ ๋ก๋ํ๊ณ  ์ ์ฅํ๋ ์ผ์ ๋ด๋นํจ

- **LogoutFilter**

๋ก๊ทธ์์ URL๋ก ์ง์ ๋ ๊ฐ์URL์ ๋ํ ์์ฒญ์ ๊ฐ์ํ๊ณ  ๋งค์นญ๋๋ ์์ฒญ์ด ์์ผ๋ฉด ์ฌ์ฉ์๋ฅผ ๋ก๊ทธ์์์ํด

- **UsernamePasswordAuthenticationFilter**

์ฌ์ฉ์๋ช๊ณผ ๋น๋ฐ๋ฒํธ๋ก ์ด๋ค์ง ํผ๊ธฐ๋ฐ ์ธ์ฆ์ ์ฌ์ฉํ๋ ๊ฐ์ URL์์ฒญ์ ๊ฐ์ํ๊ณ  ์์ฒญ์ด ์์ผ๋ฉด ์ฌ์ฉ์์ ์ธ์ฆ์ ์งํํจ

- **DefaultLoginPageGeneratingFilter**

ํผ๊ธฐ๋ฐ ๋๋ OpenID ๊ธฐ๋ฐ ์ธ์ฆ์ ์ฌ์ฉํ๋ ๊ฐ์URL์ ๋ํ ์์ฒญ์ ๊ฐ์ํ๊ณ  ๋ก๊ทธ์ธ ํผ ๊ธฐ๋ฅ์ ์ํํ๋๋ฐ ํ์ํ HTML์ ์์ฑํจ

- **BasicAuthenticationFilter**

HTTP ๊ธฐ๋ณธ ์ธ์ฆ ํค๋๋ฅผ ๊ฐ์ํ๊ณ  ์ด๋ฅผ ์ฒ๋ฆฌํจ

- **RequestCacheAwareFilter**

๋ก๊ทธ์ธ ์ฑ๊ณต ์ดํ ์ธ์ฆ ์์ฒญ์ ์ํด ๊ฐ๋ก์ฑ์ด์ง ์ฌ์ฉ์์ ์๋ ์์ฒญ์ ์ฌ๊ตฌ์ฑํ๋๋ฐ ์ฌ์ฉ๋จ SecurityContextHolderAwareRequestFilter HttpServletRequest๋ฅผHttpServletRequestWrapper๋ฅผ ์์ํ๋ ํ์ ํด๋(SecurityContextHolderAwareRequestWrapper)๋ก ๊ฐ์ธ์ ํํฐ ์ฒด์ธ์ ํ๋จ์ ์์นํ ์์ฒญ ํ๋ก์ธ์์ ์ถ๊ฐ ์ปจํ์คํธ๋ฅผ ์ ๊ณตํจ

- **AnonymousAuthenticationFilter**

์ด ํํฐ๊ฐ ํธ์ถ๋๋ ์์ ๊น์ง ์ฌ์ฉ์๊ฐ ์์ง ์ธ์ฆ์ ๋ฐ์ง ๋ชปํ๋ค๋ฉด ์์ฒญ ๊ด๋ จ ์ธ์ฆ ํ ํฐ์์ ์ฌ์ฉ์๊ฐ ์ต๋ช ์ฌ์ฉ์๋ก ๋ํ๋๊ฒ ๋จ

- **SessionManagementFilter**

์ธ์ฆ๋ ์ฃผ์ฒด๋ฅผ ๋ฐํ์ผ๋ก ์ธ์ ํธ๋ํน์ ์ฒ๋ฆฌํด ๋จ์ผ ์ฃผ์ฒด์ ๊ด๋ จํ ๋ชจ๋  ์ธ์๋ค์ด ํธ๋ํน๋๋๋ก ๋์

- **ExceptionTranslationFilter**

์ด ํํฐ๋ ๋ณดํธ๋ ์์ฒญ์ ์ฒ๋ฆฌํ๋ ๋์ ๋ฐ์ํ  ์ ์๋ ๊ธฐ๋ํ ์์ธ์ ๊ธฐ๋ณธ ๋ผ์ฐํ๊ณผ ์์์ ์ฒ๋ฆฌํจ

- **FilterSecurityInterceptor**

์ด ํํฐ๋ ๊ถํ๋ถ์ฌ์ ๊ด๋ จํ ๊ฒฐ์ ์ AccessDecisionManager์๊ฒ ์์ํด ๊ถํ๋ถ์ฌ ๊ฒฐ์  ๋ฐ ์ ๊ทผ ์ ์ด ๊ฒฐ์ ์ ์ฝ๊ฒ ๋ง๋ค์ด ์ค

[์ฐธ๊ณ ](https://devuna.tistory.com/55)
