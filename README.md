<p align="center">
  <a href="https://deezegg.com" target="_blank">
    <img src="https://i.ibb.co/1GnQZWKH/Sem-T-tulo-1-copiar.png" alt="Deez Logo" width="800">
  </a>
</p>


# 🎬 Ambarks Deez

O **Deez** é uma plataforma de rede social moderna e de alta performance, projetada para o compartilhamento de vídeos curtos. O projeto foca em oferecer uma experiência fluida de interação social, combinando tecnologias de ponta para garantir escalabilidade, segurança e interatividade em tempo real.

---

## 🚀 O Projeto?

O Deez é um ecossistema social completo que permite aos usuários criar, visualizar e interagir com conteúdos audiovisuais. Inspirado nas dinâmicas de plataformas como Shorts e Reels, ele integra funcionalidades sociais robustas com um sistema de monetização e moderação inteligente.

### Principais Funcionalidades:
- **Engine Social**: Sistema completo de postagens de vídeo, comentários e respostas (nested replies).
- **Interação Dinâmica**: Reações personalizadas (Likes, Risadas, Sad, Angry, etc.) com contadores denormalizados para performance extrema.
- **Mentions & Tags**: Sistema de marcação de usuários (@mentions) integrado e otimizado para busca case-insensitive.
- **Gamificação e Status**: Badges de perfil, frames personalizados e sistema de usuários Premium/Apoiadores.
- **Notificações em Tempo Real**: Alertas instantâneos via WebSockets e Push Notifications para manter o engajamento.
- **Monetização**: Integração nativa com gateways de pagamento (AbacatePay e Asaas).
- **Lhama (Moderação via IA)**: Motor de inteligência artificial integrado para análise e moderação automática de conteúdos (Textos, Imagens e Vídeos), garantindo um ambiente seguro e livre de spam ou conteúdos impróprios.

---

## 🛡️ Segurança e Moderação (Ambarks Lhama)

A integridade da plataforma é mantida pelo **Lhama**, um sistema de IA especializado em moderação de conteúdo multimídia criado pela Ambarks Studios:
- **Texto**: Filtra spam, links maliciosos e linguagem imprópria em comentários e descrições.
- **Imagens e Vídeos**: Analisa frames em busca de conteúdos que violem as diretrizes da comunidade, agindo de forma preventiva antes mesmo da ampla distribuição do conteúdo.
- **Processamento Assíncrono**: A integração com o Lhama ocorre via Jobs, garantindo que a análise pesada não afete o tempo de upload percebido pelo usuário.

---

## ⚙️ Como funciona? (Arquitetura)

A aplicação segue uma arquitetura moderna voltada para a redução de latência e otimização de recursos de hardware.

### Fluxo de Dados e Lógica:
- **Backend Core**: Construído sobre o **Laravel 11**, utilizando as funcionalidades mais recentes do PHP 8.4. O núcleo gerencia a lógica de negócios, autenticação e a API social.
- **Frontend Reativo**: Utiliza **Livewire 3.6** e **Alpine.js**, permitindo uma interface altamente reativa e "single-page feel" sem a complexidade de frameworks JavaScript pesados.
- **Sincronização de Dados**: O projeto utiliza uma estratégia de **denormalização** para contadores (likes, views, comentários). Isso significa que, em vez de o banco de dados contar registros toda vez que um post é aberto, ele lê valores físicos pré-calculados e indexados, garantindo carregamento instantâneo.
- **Processamento em Segundo Plano**: Tarefas pesadas (como envio de e-mails, processamento de notificações e integrações externas) são delegadas para **Filas (Queues)** gerenciadas pelo Redis, garantindo que o usuário nunca sofra com lentidão.
- **Cache Inteligente**: Uso agressivo de **Redis** para armazenar metadados de posts e perfis, reduzindo a carga no banco de dados principal.

---

## 🏗️ Infraestrutura

A infraestrutura do Deez foi projetada para ser agnóstica a nuvem e extremamente resiliente, utilizando contêineres para padronização.

### Stack Tecnológica:
- **Runtime**: **FrankenPHP** (Servidor PHP de alta performance escrito em Go, baseado no Caddy) que oferece suporte nativo a HTTP/3 e Early Hints.
- **Banco de Dados**: **MySQL 8.0** com estrutura de índices otimizada para feeds sociais e busca textual.
- **Cache & Filas**: **Redis** (Alpine version) atuando como broker de mensagens e armazenamento de estado temporário.
- **Armazenamento Híbrido**: Integração com múltiplos provedores S3 (**Wasabi, Magalu S3**) e **ImageKit** para entrega otimizada de assets.
- **Streaming**: Entrega de vídeo via **Bunny.net Stream**, garantindo baixa latência global.
- **Containerização**: Toda a stack é orquestrada via **Docker Compose**, garantindo que o ambiente de desenvolvimento seja uma cópia fiel da produção.

---

## 💎 Diferenciais Técnicos
- **SQL Tuning**: Queries otimizadas via JOINs em massa e índices compostos.
- **Case-Insensitive search**: Busca de usuários otimizada em nível de Collation de banco de dados, ignorando a necessidade de funções de string lentas como `LOWER()`.
- **Atomic Operations**: Uso de `increment()` e `decrement()` no banco de dados para evitar condições de corrida em contadores sociais.
