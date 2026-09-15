# Casinha das Letras — Plataforma 2026-27
**Plataforma de Gestão Escolar | 105 Alunos | Supabase + Netlify + Vendus API | Portal Pais | ANGOSPILLA**

> **NIF:** 5001019864 | **Nº 2230** | **Email:** casinhadasletras.ccl@gmail.com | **Tel:** +244 931 347 717  
> **Endereço:** Rua Comandante Dack Doy, Bairro Azul, Ingombota, Luanda  
> **Software desenvolvido por ANGOSPILLA Soluções & E • Nº 2230 • NIF 5001019864 - Logo singelo 32px**

## 🚀 Demo ao Vivo
- **Netlify:** https://casinhadasletras.netlify.app
- **Supabase:** https://vxtxabbjlxirrbgkctqn.supabase.co
- **Vendus API:** https://www.vendus.co.ao/ws/v1.1/ (Validado Nº 142/AGT Angola)

## 📦 O que tem neste repo
- `index.html` - **Final único**: Portal Pais + Recibo 000245 com carimbo + QR Vendus + Letrinha animada + Footer ANGOSPILLA singelo 32px
- `assets/`:
  - `logo_casinha_enquadrado_grande.jpg` - logo grande 280px (não pequeno)
  - `ANGOSPILLA_LOGO.png` - logo singelo 32px footer
  - `MASCOTE_-_Casinha_das_Letras.png` - Letrinha menina negra tranças azul livro verde
  - `financeiro_data.json` - 105 alunos (base, transporte, ballet, jiu, bilíngue, total)
- `reparo-duplicados-casinha.html` - ferramenta fusão duplicados (upsert por nome, move encarregados/faturas/avaliacoes)
- `modelos_xlsx/` - Modelos Importação Financeira CORRETO aba Importacao + Clientes Vendus + Produtos + Faturas + Presenças Mensal

## ✨ Funcionalidades
1. **1º ao 6º Ano + Pré + Iniciação + NEE** - Planos semanais, horários 8:00-12:35 Lanche 9:40-10:00, Tarefas Gerais 7-11 e 14-18 Setembro, VAMOS TRAÇAR? A ABELHA 🐝 etc
2. **Ficha Aluno + Portal Pais** - 7 abas: Dados+QR CASINHA|MAT|NOME|TURMA|NIF, Aulas, Grade Curricular, Material, Tarefas, Pessoas Autorizadas Mãe Pai Avó Maria de Lurdes Tia Sofia Mendes, Financeiro
3. **6 Documentos Oficiais** - 01 Ficha Matrícula, 02 Mapa Mensal Presenças P verde F vermelho J amarelo A azul, 03 Declaração Frequência, 04 Relatório Individual, 05 Autorização Visita Museu Nacional Angola, 06 Recibo Pagamento 000245 + Boletins + Diplomas
4. **Letrinha Animada** - bottom 20px right 20px 150px animation letrinhaMovimento 3s, bolha fala, FAQ 35+ Q&A pt-AO, email casinhadasletras.ccl@gmail.com
5. **Vendus CEGID API** - POST /clients/, /products/, /documents/, GET /documents/{id}.pdf, SAF-T, bulk 105 Faturas-Recibo
6. **Recibo Oficial 000245** - carimbo circular azul Casinha Luanda Angola + QR VENDUS|RECIBO|000245|...|VALIDO-AGT-142 + PDF + Email + WhatsApp
7. **Migração XLSX** - Importar XLSX → Vendus upsert por nome, Exportar Vendus → XLSX SheetJS, Modelos
8. **Footer ANGOSPILLA singelo 32px** - <img height=32> + Software desenvolvido por ANGOSPILLA Soluções & E • Nº 2230 • NIF 5001019864

## 🛠️ Deploy

### Netlify Drop (30s)
1. Baixa o ZIP `CASINHA_LETRAS_index_plus_assets.zip`
2. Vai em https://app.netlify.com/drop
3. Arrasta index.html + assets/
4. Site no ar em casinhadasletras.netlify.app

Env vars Netlify:
```
VITE_SUPABASE_URL=https://vxtxabbjlxirrbgkctqn.supabase.co
VITE_SUPABASE_ANON_KEY=sb_publishable_Ss3YMudwL2t71qnqhdeQVw_O7weUiwo
VITE_VENDUS_API_KEY=sua_key
VITE_VENDUS_BASE=https://www.vendus.co.ao/ws/v1.1/
VITE_EMAIL=casinhadasletras.ccl@gmail.com
```

### Supabase SQL
Corre no SQL Editor:
```sql
DROP POLICY IF EXISTS "direcao pode apagar alunos" ON alunos;
CREATE POLICY "direcao pode apagar alunos" ON alunos FOR DELETE TO authenticated USING (get_my_role() IN ('direcao'));

CREATE TABLE IF NOT EXISTS faturas (id uuid primary key default gen_random_uuid(), aluno_id uuid references alunos(id), numero text, recibo_numero text, total numeric, metodo text, data_pagamento date default current_date, vendus_id text, vendus_pdf_url text, status text default 'Pago', created_at timestamptz default now());
CREATE TABLE IF NOT EXISTS documentos_oficiais (id uuid primary key default gen_random_uuid(), aluno_id uuid references alunos(id), tipo text, numero text, conteudo jsonb, qr_code text, vendus_validado boolean default false, created_at timestamptz default now());
CREATE TABLE IF NOT EXISTS presencas_mensal (id uuid primary key default gen_random_uuid(), aluno_id uuid references alunos(id), mes int, ano int, dias jsonb, total int, presencas int, created_at timestamptz default now());
```

### GitHub
```bash
git clone https://github.com/angospilla-lang/Casinha-das-Letras---Plataforma-2026-27.git
cd Casinha-das-Letras---Plataforma-2026-27
# copia index.html + assets/
git add .
git commit -m "feat: Portal Pais + Recibo 000245 Vendus + Letrinha + Footer ANGOSPILLA singelo 32px + 105 alunos"
git push origin main
```

## 📋 Cores
- vermelho #C0392B, amarelo #F4B400, azul #2E6DA4, creme #FFFCF5, dark blue #0F2D52, mint #E8F5E9

© 2026 Casinha das Letras - Aprender hoje, feliz amanhã | ANGOSPILLA Prestação de Serviços (SU), LDA.
