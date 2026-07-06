# GitHub – Require Code Quality Results (Java)

## O que é?

A opção **"Require code quality results"** do GitHub permite bloquear o merge de Pull Requests com base em problemas identificados pela análise de qualidade de código (GitHub Code Quality / CodeQL). Ela não é uma métrica de cobertura de testes e também não é apenas um linter tradicional. [1](https://docs.github.com/en/code-security/how-tos/maintain-quality-code/set-pr-thresholds)[2](https://docs.github.com/en/code-security/concepts/about-code-quality)

## Níveis de severidade

É possível definir qual severidade impedirá o merge do Pull Request. [1](https://docs.github.com/en/code-security/how-tos/maintain-quality-code/set-pr-thresholds)

- **Errors** → bloqueia apenas problemas classificados como erro.
- **Warnings and higher** → bloqueia warnings e errors.
- **Notes and higher** → bloqueia notes, warnings e errors.

### Exemplo

```text
Require code quality results
Severity: Warnings and higher
```

Neste cenário, qualquer Pull Request contendo um warning ou error não poderá ser mergeado. [1](https://docs.github.com/en/code-security/how-tos/maintain-quality-code/set-pr-thresholds)

---

# Qualidade para Projetos Java

Geralmente a estratégia de qualidade é dividida em três pilares:

## 1. Coverage (Cobertura de Testes)

Mede quanto do código está sendo exercitado pelos testes automatizados.

### Ferramentas

- JaCoCo
- GitHub Coverage Reports
- SonarQube Coverage

### Exemplo de regra

```text
Coverage >= 80%
```

O GitHub também suporta políticas de cobertura separadas das regras de Code Quality. [2](https://docs.github.com/en/code-security/concepts/about-code-quality)[3](https://github.blog/changelog/2026-06-16-github-code-quality-generally-available-july-20-2026/)

---

## 2. Linter / Code Style

Valida padrões de desenvolvimento e convenções de código.

### Ferramentas Java

- Checkstyle
- PMD
- Spotless
- Error Prone

### Exemplos de validação

```text
- Imports não utilizados
- Nome de variável fora do padrão
- Formatação inconsistente
- Violação de convenções de código
```

---

## 3. Static Analysis / Quality Gate

Analisa problemas de qualidade, bugs potenciais e maintainability.

### Ferramentas

- SonarQube
- SonarCloud
- GitHub Code Quality
- CodeQL

### Exemplos

```text
- Possível NullPointerException
- Código duplicado
- Complexidade excessiva
- Métodos muito grandes
- Problemas de manutenibilidade
```

---

# Recomendação para Times Java

Uma configuração corporativa comum é:

```text
✅ Require pull request reviews

✅ Require status checks:
   - Build (Maven/Gradle)
   - Unit Tests
   - JaCoCo Coverage >= 80%
   - SonarQube Quality Gate = Passed
   - GitHub Code Quality = Warnings and higher
```

## Quando usar SonarQube?

Se o projeto já utiliza **SonarQube** ou **SonarCloud**, normalmente o principal bloqueio de qualidade fica no **Sonar Quality Gate**, enquanto o GitHub Code Quality funciona como complemento. [1](https://docs.github.com/en/code-security/how-tos/maintain-quality-code/set-pr-thresholds)[2](https://docs.github.com/en/code-security/concepts/about-code-quality)

---

# Resumo

| Categoria | Ferramenta Recomendada |
|------------|------------------------|
| Coverage | JaCoCo |
| Linter | Checkstyle, PMD |
| Static Analysis | SonarQube, SonarCloud |
| GitHub Quality Gate | GitHub Code Quality / CodeQL |

## Conclusão

A opção **"Require code quality results"** está mais próxima de um **Quality Gate de análise estática (SonarQube/CodeQL)** do que de uma ferramenta de cobertura de testes ou de linting simples. [1](https://docs.github.com/en/code-security/how-tos/maintain-quality-code/set-pr-thresholds)[2](https://docs.github.com/en/code-security/concepts/about-code-quality)
