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

# Informações auditadas 

 * ID -> Chave única e sequencial da tabela de auditoria, o que permite a indentificação de registros excluídos em casos de fraude
 * DATA_OPERACAO -> Data, hora, minuto e segundo da ocorrência da transação no banco
 * USUARIO_PC -> Informações fonecidas pela camada de aplicação através do CONTEXT_INFO()
 * USUARIO_APP -> Nome do usuário ou aplicação responsável pela conexão obtido através do HOST_NAME()
 * TABELA -> Identificação da tabela que sofreu alteração na base auditada
 * OPERACAO -> Identificação do tipo de operação realizada (insert,update,delete)
 * OLD_DATA -> Snapshot dos dados da tabela antes da alteração realizada 
 * NEW_DATA -> Snapshot dos dados da tabela após alteração realizada
 * USUARIO_DB -> Nome do usuário de conexão na base de dados obtido através do SUSER_NAME() 

# Vantagens do processo

 * Permite o isolamento da camada de auditoria, garantindo que toda transação realizada a nível de banco seja analisada, independente de aplicão conectada
 * Permite a retenção das informações de auditoria em base independente, o que facilita processos de criptografia em paralelo
 * Facilita a manutenção dos gatilhos, tornando desnecessárias implementações adicionais na camada de aplicação quando ocorre a incorporação de novos campos ou novas entidades
 * Facilita o uso dos dados em ferramentas de análise, pois as informações são armazenadas em formato JSON, comumente utilizado na maioria dos frameworks destinados ao desenvolvimento de frontend 
 * Facilita a recuperação pontual de informações que possam ter sido alteradas de forma indevida, retendo o status do registro antes e depois da alteração

# Informações adicionais

 * As informações dos dados são armazenados em formato JSON, nativo do SQL Server superior a 2016
 * Para versões do SQL Server anteriores a 2016 é possível a adaptação do processo de auditoria para uso de dados no formato XML
