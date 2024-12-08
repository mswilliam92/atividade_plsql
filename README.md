# PLSQL
Organizando todos os comandos e pacotes em entrega de atividade de Gerenciamento de Banco de dados

## Estrutura do Banco de Dados

O banco de dados contém as seguintes tabelas:

1. **PROFESSORES**: Contém informações sobre os professores.
   - **ID**: Identificador único do professor.
   - **NOME**: Nome do professor.

2. **TURMAS**: Contém informações sobre as turmas que os professores lecionam.
   - **ID**: Identificador único da turma.
   - **ID_PROFESSOR**: Chave estrangeira que faz referência ao professor responsável pela turma.

3. **DISCIPLINAS**: Contém informações sobre as disciplinas lecionadas pelos professores.
   - **ID**: Identificador único da disciplina.
   - **ID_PROFESSOR**: Chave estrangeira que faz referência ao professor responsável pela disciplina.

4. **ALUNOS**: Contém informações sobre os alunos.
   - **ID**: Identificador único do aluno.
   - **NOME**: Nome do aluno.

5. **MATRICULAS**: Contém informações sobre as matrículas dos alunos em disciplinas e turmas.
   - **ID**: Identificador único da matrícula.
   - **ID_ALUNO**: Chave estrangeira que faz referência ao aluno.
   - **ID_DISCIPLINA**: Chave estrangeira que faz referência à disciplina.
   - **ID_TURMA**: Chave estrangeira que faz referência à turma.
   - **NOTA**: Nota do aluno na disciplina.

## Pacotes PL/SQL

### 1. **PKG_PROFESSOR**

Este pacote contém funções relacionadas aos professores.

#### Funções:
- **TOTAL_TURMAS_POR_PROFESSOR**: Retorna o número de turmas que cada professor leciona, considerando apenas aqueles que lecionam mais de uma turma.
    - **Exemplo de uso**:
      ```sql
      EXEC PKG_PROFESSOR.TOTAL_TURMAS_POR_PROFESSOR;
      ```

- **TOTAL_TURMAS_PROFESSOR**: Retorna o número total de turmas que um professor específico leciona.
    - **Parâmetro**: `P_ID_PROFESSOR` (ID do professor).
    - **Exemplo de uso**:
      ```sql
      DECLARE
          v_total NUMBER;
      BEGIN
          v_total := PKG_PROFESSOR.TOTAL_TURMAS_PROFESSOR(1);
          DBMS_OUTPUT.PUT_LINE(v_total);
      END;
      ```

- **PROFESSOR_DISCIPLINA**: Retorna o nome do professor responsável por uma disciplina específica.
    - **Parâmetro**: `P_ID_DISCIPLINA` (ID da disciplina).
    - **Exemplo de uso**:
      ```sql
      DECLARE
          v_nome VARCHAR2(100);
      BEGIN
          v_nome := PKG_PROFESSOR.PROFESSOR_DISCIPLINA(1);
          DBMS_OUTPUT.PUT_LINE(v_nome);
      END;
      ```

### 2. **PKG_ALUNO**

Este pacote contém funções relacionadas aos alunos.

#### Funções:
- **TOTAL_DISCIPLINAS_POR_ALUNO**: Retorna o número total de disciplinas em que um aluno está matriculado.
    - **Parâmetro**: `P_ID_ALUNO` (ID do aluno).
    - **Exemplo de uso**:
      ```sql
      DECLARE
          v_total NUMBER;
      BEGIN
          v_total := PKG_ALUNO.TOTAL_DISCIPLINAS_POR_ALUNO(1);
          DBMS_OUTPUT.PUT_LINE(v_total);
      END;
      ```

- **MEDIA_NOTAS_ALUNO**: Retorna a média das notas de um aluno nas disciplinas em que está matriculado.
    - **Parâmetro**: `P_ID_ALUNO` (ID do aluno).
    - **Exemplo de uso**:
      ```sql
      DECLARE
          v_media NUMBER;
      BEGIN
          v_media := PKG_ALUNO.MEDIA_NOTAS_ALUNO(1);
          DBMS_OUTPUT.PUT_LINE(v_media);
      END;
      ```

- **ALUNOS_TURMA**: Retorna uma lista de alunos matriculados em uma turma específica.
    - **Parâmetro**: `P_ID_TURMA` (ID da turma).
    - **Exemplo de uso**:
      ```sql
      DECLARE
          v_cursor SYS_REFCURSOR;
          v_nome VARCHAR2(100);
      BEGIN
          v_cursor := PKG_ALUNO.ALUNOS_TURMA(1);
          LOOP
              FETCH v_cursor INTO v_nome;
              EXIT WHEN v_cursor%NOTFOUND;
              DBMS_OUTPUT.PUT_LINE(v_nome);
          END LOOP;
          CLOSE v_cursor;
      END;
      ```

### 3. **PKG_DISCIPLINA**

Este pacote contém funções relacionadas às disciplinas.

#### Funções:
- **PROFESSORES_POR_DISCIPLINA**: Retorna os professores responsáveis por uma disciplina específica.
    - **Parâmetro**: `P_ID_DISCIPLINA` (ID da disciplina).
    - **Exemplo de uso**:
      ```sql
      DECLARE
          v_cursor SYS_REFCURSOR;
          v_nome VARCHAR2(100);
      BEGIN
          v_cursor := PKG_DISCIPLINA.PROFESSORES_POR_DISCIPLINA(1);
          LOOP
              FETCH v_cursor INTO v_nome;
              EXIT WHEN v_cursor%NOTFOUND;
              DBMS_OUTPUT.PUT_LINE(v_nome);
          END LOOP;
          CLOSE v_cursor;
      END;
      ```

- **TOTAL_ALUNOS_POR_DISCIPLINA**: Retorna o número de alunos matriculados em uma disciplina específica.
    - **Parâmetro**: `P_ID_DISCIPLINA` (ID da disciplina).
    - **Exemplo de uso**:
      ```sql
      DECLARE
          v_total NUMBER;
      BEGIN
          v_total := PKG_DISCIPLINA.TOTAL_ALUNOS_POR_DISCIPLINA(1);
          DBMS_OUTPUT.PUT_LINE(v_total);
      END;
      ```

- **MEDIA_NOTA_DISCIPLINA**: Retorna a média das notas dos alunos de uma disciplina específica.
    - **Parâmetro**: `P_ID_DISCIPLINA` (ID da disciplina).
    - **Exemplo de uso**:
      ```sql
      DECLARE
          v_media NUMBER;
      BEGIN
          v_media := PKG_DISCIPLINA.MEDIA_NOTA_DISCIPLINA(1);
          DBMS_OUTPUT.PUT_LINE(v_media);
      END;
      ```
