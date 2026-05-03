# letech-gestao-docs
Documentação e portfólio do sistema Letech Gestão — sistema de gestão empresarial desenvolvido para a Letech Energia.
# Letech Gestão — Sistema de Gestão Empresarial

> Sistema interno desenvolvido para a **Letech Energia** (Letech Serviços e Comércio Ltda), 
> empresa de serviços e locação de equipamentos elétricos com atuação em todo o Brasil.

---

## 🎯 O Projeto

A Letech Energia não possuía um sistema de gestão integrado. 
Todas as informações eram controladas em planilhas, blocos de notas e ferramentas 
desconectadas entre si — o que gerava retrabalho, erros e falta de visibilidade para a diretoria.

O **Letech Gestão** foi desenvolvido do zero para centralizar toda a operação da empresa 
em um único sistema web, acessível por todos os perfis de usuário com níveis de permissão distintos.

---

## 🏢 A Empresa

- **Nome:** Letech Energia
- **Atuação:** Todo o Brasil
- **Segmento:** Serviços elétricos e locação de equipamentos de medição
- **Regime tributário:** Simples Nacional

---

## 🛠️ Stack Tecnológica

| Tecnologia | Uso |
|---|---|
| React + TypeScript | Frontend |
| Tailwind CSS | Estilização |
| Vite | Build tool |
| Supabase (PostgreSQL) | Banco de dados + Auth + Storage |
| Vercel | Hospedagem e deploy automático |
| GitHub | Controle de versão |

---

## 🏗️ Arquitetura

**Decisões arquiteturais:**
- **Supabase** escolhido pela combinação de banco PostgreSQL + autenticação + storage + RLS em um único serviço
- **RLS (Row Level Security)** implementado em todas as tabelas — cada perfil vê apenas o que deve ver
- **Soft-delete** como padrão global — nenhum registro é deletado, apenas desativado (`ativo = false`)
- **Regime de competência** como critério único para relatórios e dashboards
- **Deploy automático** — cada `git push` na branch `main` publica em produção automaticamente

---

## 👥 Perfis de Usuário

| Perfil | Acesso |
|---|---|
| Diretor | Acesso completo |
| Gerente Operacional | Acesso completo |
| Administrativo | Acesso completo |
| Relatório Técnico | OS + Relatórios |
| Técnico | OS + Gastos + Quilometragem (mobile) |
| Almoxarifado | Estoque |
| Contador | Visão contábil (somente leitura) |

---

## 📋 Módulos Desenvolvidos

| Módulo | Status | Descrição |
|---|---|---|
| Autenticação + Dashboard | ✅ | Login por perfil, dashboard personalizado |
| Clientes | ✅ | Cadastro com tipo (serviço/locação/ambos) |
| Propostas | ✅ | Serviço, obra e locação com numeração automática |
| Ordens de Serviço | ✅ | Controle completo de OS com gastos e quilometragem |
| Financeiro | ✅ | Fluxo de caixa, DRE, contas recorrentes |
| Frota | ✅ | Veículos, manutenções, quilometragem |
| Equipamentos | ✅ | Cadastro, calibrações, QR Code |
| Estoque | ✅ | Movimentações, devoluções, mínimo de estoque |
| **Locações** | ✅ | Locação de equipamentos com prorrogação, checklist e notificações |
| Relatórios de Execução | ⏳ | Em desenvolvimento |
| Geração de PDF | ⏳ | Propostas e faturas de locação |
| Dashboard dados reais | ⏳ | Em desenvolvimento |
| Otimização mobile | ⏳ | Foco nos técnicos em campo |
| PWA | 🔮 | Planejado — suporte offline para técnicos |

---

## 🔐 Segurança

- Autenticação via Supabase Auth (JWT)
- RLS ativo em todas as tabelas
- Variáveis de ambiente protegidas (nunca expostas no código)
- Repositório do código fonte privado
- URLs assinadas para arquivos privados (certificados, comprovantes, relatórios)

---

## 🧠 Decisões Técnicas Relevantes

### Regime de Competência
Todos os relatórios e dashboards usam a data de início/competência como referência, nunca a data de pagamento. Isso garante consistência entre módulos e alinhamento com práticas contábeis.

### Soft-Delete
Nenhum registro é deletado do banco. Sempre `ativo = false`. Isso garante rastreabilidade total e evita perda acidental de dados.

### Numeração de Prorrogações
Locações prorrogadas seguem numeração baseada sempre na locação raiz:
- Locação original: `178`
- 1ª prorrogação: `178_1`
- 2ª prorrogação: `178_2` (nunca `178_1_1`)

### Notificações Automáticas
Cron jobs no Supabase notificam automaticamente gestores sobre:
- Contas vencendo hoje
- Locações ativas sem confirmação de pagamento há mais de 3 dias
- Calibrações próximas do vencimento

### Multi-perfil com RLS
Cada tabela tem policies específicas por perfil. Técnicos não veem valores financeiros. Contador tem acesso somente leitura à visão contábil.

---

## 🚀 Como Rodar Localmente

```bash
git clone https://github.com/letech-energy/letech-flow-hub.git
cd letih-flow-hub
bun install
bun dev
```

**.env necessário:**

> ⚠️ Repositório do código fonte é privado. Este repositório contém apenas documentação.

---

## 👨‍💻 Desenvolvedor

**Danilo Silva**
- GitHub: [@irmones](https://github.com/irmones)
- Email: dasilva.danilo1@gmail.com

> Sistema desenvolvido integralmente por Danilo Silva, 
> desde a arquitetura do banco de dados até o frontend,
> utilizando React, TypeScript, Supabase e boas práticas de desenvolvimento.

---

## 📸 Screenshots

*Em breve — aguardando conclusão dos módulos restantes.*

---

*Letech Energia - #padraoletech*

