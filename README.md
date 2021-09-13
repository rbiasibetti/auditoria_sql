# Auditoria MS SQL Sever
Processo de auditoria na camada de banco de dados desenvolvido em 2019 abstarindo a necessidade de interceptor na camada de aplicação, dando maior flexibilidade e autonomia ao processo.

O processo consiste em:
 * Criação de função com finalidade de separar elementos contatenados oriundos da camada de aplicação. (SEPARAR)
 * Criação de base independente e destinada a retenção dos logs de auditoria. (base AUDITORIA)
 * Adequação de tipos de dados a fim de compatibilizar o processo de auditoria. (SP_AJUSTATIPOS)
 * Criação de uma procedure centralizada a fim de facilitar a manutenção e vinculação do processo de auditoria.(SP_CRIATRIGGERSAUDITORIA)
 * Atribuição de gatilhos de monitoração em todas as tabelas de um banco de dados específico.(TRIGGER TRG_AUD_*)
 * Criação de view para consulta das informações retinas na base de auditoria.(VW_AUDITORIA)
 * Definição e atribuição dos parâmetros da camada de aplicação.(uso do CONTEXT_INFO na camada de aplicação)
