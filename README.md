# Planejamento da Stack Tecnológica

Este documento descreve as tecnologias sugeridas para o desenvolvimento do sistema, focando em alta performance, consistência de dados e escalabilidade.

## Arquitetura Sugerida

| Componente | Sugestão | Por que? |
| :--- | :--- | :--- |
| **Linguagem** | Node.js (TypeScript) ou Go | Alta performance para I/O e concorrência. |
| **Banco de Dados Principal** | PostgreSQL | Suporte robusto a transações ACID (evita double-booking). |
| **Cache & Lock** | Redis | Gerenciamento de reserva temporária de horários. |
| **Mensageria** | RabbitMQ ou Kafka | Processamento de notificações assíncronas sem travar a API. |
| **Infraestrutura** | Docker + Kubernetes | Escalabilidade e facilidade de deploy. |

## Detalhes de Implementação

1. **Consistência:** O uso do PostgreSQL garante que dois usuários não consigam agendar o mesmo horário simultaneamente através de transações.
2. **Performance:** O Redis atua como uma camada de bloqueio rápido (Distributed Lock), segurando o horário por alguns minutos enquanto o usuário preenche os dados de pagamento.
3. **Escalabilidade:** A infraestrutura em containers permite que o sistema cresça conforme a demanda de acessos aumenta.
