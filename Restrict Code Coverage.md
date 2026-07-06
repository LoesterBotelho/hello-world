# GitHub – Restrict Code Coverage (Java / Spring Boot)

## Objetivo

A regra **"Restrict code coverage"** do GitHub permite bloquear o merge de Pull Requests quando a cobertura de testes não atende aos limites mínimos definidos para o repositório. A cobertura enviada pelos pipelines deve satisfazer os critérios configurados antes da aprovação do merge. [1](https://docs.github.com/en/code-security/concepts/about-code-quality)[2](https://github.blog/changelog/2026-06-16-github-code-quality-generally-available-july-20-2026/)

---

## Recomendação para Java + Spring Boot

### Cobertura mínima

```text
Minimum Coverage: 80%
```

ou

```text
Coverage >= 0.80
```

### Justificativa

- 80% é frequentemente adotado como baseline corporativo.
- Permite boa proteção contra regressões.
- Evita exigir 100%, o que normalmente gera alto custo de manutenção e pouco ganho prático.
- Funciona bem para APIs Spring Boot, serviços, componentes e regras de negócio.

---

## Ferramenta recomendada

### JaCoCo

O JaCoCo é o padrão mais utilizado para medir cobertura em projetos Java/Spring.

Exemplo Maven:

```xml
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <version>0.8.12</version>
</plugin>
```

O relatório gerado pelo JaCoCo pode ser enviado para:

- GitHub Code Coverage
- SonarQube
- SonarCloud

---

## Configuração recomendada

```text
Require pull request reviews

Require status checks:
✅ Build
✅ Unit Tests
✅ Code Quality Results
✅ Code Coverage
```

### Coverage Policy

```text
Minimum Coverage: 80%

OR

Coverage cannot decrease by more than 2%
```

---

## Quality Gate Completo para Spring Boot

```text
Build: PASS

Unit Tests: PASS

Coverage:
  >= 80%

SonarQube:
  Quality Gate = PASS

GitHub Code Quality:
  Severity = Warnings and higher
```

---

## Exemplo de Política

```text
Branch: main

Require code quality results:
  Warnings and higher

Restrict code coverage:
  Minimum coverage = 80%

Require status checks:
  - Maven Build
  - Unit Tests
  - JaCoCo Coverage
  - SonarQube Quality Gate
```

---

## Resumo

Para projetos **Java + Spring Boot**, a configuração recomendada é:

```text
Coverage (JaCoCo): 80%
Code Quality: Warnings and higher
Build: obrigatório
Unit Tests: obrigatórios
SonarQube Quality Gate: obrigatório
```

✅ Cobertura mínima recomendada: **0.80 (80%)**
✅ Ferramenta recomendada: **JaCoCo**
✅ Integração opcional: **SonarQube/SonarCloud**
✅ Bloquear merge quando coverage < 80%
