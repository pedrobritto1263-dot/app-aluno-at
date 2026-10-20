<!doctype html>
<html lang="pt-BR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>PowerGym — Painel Aluno</title>
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&display=swap"
      rel="stylesheet"
    />
    <link
      href="https://unpkg.com/boxicons@2.1.4/css/boxicons.min.css"
      rel="stylesheet"
    />
    <link rel="stylesheet" href="style.css" />
  </head>
  <body data-page="login">
    <!-- ═══════════════════ ALUNO SHELL ═══════════════════ -->
    <div id="page-aluno" class="page">
      <aside class="sidebar" id="sidebar">
        <div class="sidebar-logo">
          <span class="brand-icon sm"><i class="bx bx-dumbbell"></i></span>
          <span class="logo-text">PowerGym</span>
        </div>
        <nav class="sidebar-nav" role="navigation" aria-label="Menu principal">
          <button
            type="button"
            class="nav-item active"
            data-section="dashboard"
            onclick="showSection(this, 'dashboard')"
            aria-current="page"
          >
            <i class="bx bx-home-alt"></i><span>Dashboard</span>
          </button>

          <button
            type="button"
            class="nav-item"
            data-section="progresso"
            onclick="showSection(this, 'progresso')"
          >
            <i class="bx bx-chart"></i><span>Meu Progresso</span>
          </button>

          <button
            type="button"
            class="nav-item"
            data-section="criar-treino"
            onclick="showSection(this, 'criar-treino')"
          >
            <i class="bx bx-plus"></i><span>Criar Treino</span>
          </button>

          <button
            type="button"
            class="nav-item"
            data-section="meus-treinos"
            onclick="showSection(this, 'meus-treinos')"
          >
            <i class="bx bx-run"></i><span>Meus Treinos</span>
          </button>

          <button
            type="button"
            class="nav-item"
            data-section="calculadoradeimc"
            onclick="showSection(this, 'calculadoradeimc')"
          >
            <i class="bx bx-calculator"></i><span>Calculadora de IMC</span>
          </button>

          <button
            type="button"
            class="nav-item"
            data-section="configuracoes"
            onclick="showSection(this, 'configuracoes')"
          >
            <i class="bx bx-cog"></i><span>Configurações</span>
          </button>
        </nav>
        <div class="sidebar-footer">
          <div class="aluno-info">
            <div class="aluno-avatar" aria-hidden="true">AL</div>
            <div>
              <p class="aluno-name">Aluno</p>
              <p class="aluno-role">aluno@powergym.com</p>
            </div>
          </div>
          <button
            type="button"
            class="btn-logout"
            onclick="doLogout()"
            title="Sair"
          >
            <i class="bx bx-log-out"></i>
          </button>
        </div>
      </aside>

      <div class="main-wrapper">
        <header class="topbar">
          <div class="topbar-left">
            <button type="button" class="menu-toggle" onclick="toggleSidebar()">
              <i class="bx bx-menu"></i>
            </button>
            <div class="breadcrumb" id="breadcrumb">Dashboard</div>
          </div>
        </header>

        <main class="content" id="main-content">
          <!-- ──── DASHBOARD ──── -->
          <section
            id="section-dashboard"
            class="section active"
            aria-labelledby="dashboard-title"
          >
            <div class="section-header">
              <h1 id="dashboard-title">Dashboard</h1>
              <p>
                Visão geral de avanço na academia —
                <span id="today-date"></span>
              </p>
            </div>
            <div class="kpi-grid">
              <div class="kpi-card">
                <div class="kpi-icon orange"><i class="bx bx-group"></i></div>
                <div>
                  <p class="kpi-label">Minha Atividade</p>
                  <p class="kpi-value" id="kpi-treinos">245</p>
                  <p class="kpi-delta up">+12 este mês</p>
                </div>
              </div>
              <div class="kpi-card">
                <div class="kpi-icon blue">
                  <i class="bx bx-user-check"></i>
                </div>
                <div>
                  <p class="kpi-label">Treinos</p>
                  <p class="kpi-value" id="kpi-treino">12</p>
                  <p class="kpi-delta">estáveis</p>
                </div>
              </div>
              <div class="kpi-card">
                <div class="kpi-icon amber">
                  <i class="bx bx-dollar-circle"></i>
                </div>
                <div>
                  <p class="kpi-label">treinos anuais</p>
                  <p class="kpi-value" id="kpi-fat">&nbsp;229 treinos</p>
                  <p class="kpi-delta up">+5% vs mês anterior</p>
                </div>
              </div>
            </div>

            <div class="dash-grid">
              <div class="dash-card">
                <div class="card-header">
                  <h3>Treinos Recentes</h3>
                  <button
                    type="button"
                    class="btn-sm"
                    onclick="
                      showSection(
                        document.querySelector('[data-section=meus-treinos]'),
                        'meus-treinos',
                      )
                    "
                  >
                    Ver todos
                  </button>
                </div>
                <table class="data-table">
                  <thead>
                    <tr>
                      <th scope="col">treino</th>
                      <th scope="col">Plano</th>
                      <th scope="col">Status</th>
                      <th scope="col">Ação</th>
                    </tr>
                  </thead>
                  <tbody id="dash-treinos-tbody"></tbody>
                </table>
              </div>
              <div class="dash-card">
                <div class="card-header">
                  <h3>Alertas do Sistema</h3>
                </div>
                <div class="alert-list">
                  <div class="alert-item warn">
                    <i class="bx bx-time-five"></i>
                    <div>
                      <p>mensalidade vencida</p>
                      <span>Vencimento nos últimos 7 dias</span>
                    </div>
                  </div>
                  <div class="alert-item success">
                    <i class="bx bx-trending-up"></i>
                    <div>
                      <p>Meta mensal de treinos atingida</p>
                      <span>25 / 25</span>
                    </div>
                  </div>
                  <div class="alert-item danger">
                    <i class="bx bx-x-circle"></i>
                    <div>
                      <p>2 alunos inadimplentes</p>
                      <span>Acima de 30 dias em atraso</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </section>

          <!-- ──── PROGRESSO ──── -->
          <section
            id="section-progresso"
            class="section"
            aria-labelledby="progresso-title"
          >
            <div class="section-header">
              <h1 id="progresso-title">Meu Progresso</h1>
              <p>Acompanhe sua evolução na academia</p>
            </div>

            <!-- KPI Cards -->
            <div class="kpi-grid">
              <div class="kpi-card">
                <div class="kpi-icon green">
                  <i class="bx bx-trending-up"></i>
                </div>
                <div>
                  <p class="kpi-label">Perda de Peso</p>
                  <p class="kpi-value" id="progress-peso-perdido">9.5 kg</p>
                  <p class="kpi-delta down">-10.3% desde início</p>
                </div>
              </div>

              <div class="kpi-card">
                <div class="kpi-icon blue">
                  <i class="bx bx-calculator"></i>
                </div>
                <div>
                  <p class="kpi-label">IMC Atual</p>
                  <p class="kpi-value" id="progress-imc">26.9</p>
                  <p class="kpi-delta">Meta: 24.0 (3.9 ↓)</p>
                </div>
              </div>

              <div class="kpi-card">
                <div class="kpi-icon amber">
                  <i class="bx bx-run"></i>
                </div>
                <div>
                  <p class="kpi-label">Treinos Realizados</p>
                  <p class="kpi-value" id="progress-treinos">18 / 24</p>
                  <p class="kpi-delta">75% da meta mensal</p>
                </div>
              </div>

              <div class="kpi-card">
                <div class="kpi-icon orange">
                  <i class="bx bx-dumbbell"></i>
                </div>
                <div>
                  <p class="kpi-label">Ganho de Força</p>
                  <p class="kpi-value" id="progress-forca">+22.5%</p>
                  <p class="kpi-delta up">Acima da meta</p>
                </div>
              </div>
            </div>

            <!-- Gráfico de Evolução -->
            <div class="progress-grid">
              <div class="progress-card">
                <h3>Evolução de Peso (últimas 3 semanas)</h3>
                <div class="chart-container">
                  <div class="bar-chart" id="chart-peso">
                    <!-- Barras serão geradas por JS -->
                  </div>
                </div>
              </div>

              <div class="progress-card">
                <h3>Metas Semanais</h3>
                <div class="meta-item">
                  <label>Treinos Semana 1</label>
                  <div class="progress-bar">
                    <div class="progress-fill" style="width: 100%"></div>
                  </div>
                  <span class="progress-text">4 / 4</span>
                </div>
                <div class="meta-item">
                  <label>Treinos Semana 2</label>
                  <div class="progress-bar">
                    <div class="progress-fill" style="width: 80%"></div>
                  </div>
                  <span class="progress-text">4 / 5</span>
                </div>
                <div class="meta-item">
                  <label>Treinos Semana 3</label>
                  <div class="progress-bar">
                    <div class="progress-fill" style="width: 100%"></div>
                  </div>
                  <span class="progress-text">5 / 5</span>
                </div>
                <div class="meta-item">
                  <label>Semana Atual</label>
                  <div class="progress-bar">
                    <div class="progress-fill" style="width: 60%"></div>
                  </div>
                  <span class="progress-text">3 / 5</span>
                </div>
              </div>
            </div>

            <!-- Histórico de Treinos -->
            <div class="progress-card">
              <h3>Últimos Treinos Realizados</h3>
              <table class="data-table" id="historico-treinos-table">
                <thead>
                  <tr>
                    <th scope="col">Exercício</th>
                    <th scope="col">Data</th>
                    <th scope="col">Séries × Reps</th>
                    <th scope="col">Carga (kg)</th>
                    <th scope="col">Duração</th>
                  </tr>
                </thead>
                <tbody id="historico-treinos-tbody">
                  <!-- Preenchido por JS -->
                </tbody>
              </table>
            </div>

            <!-- Badges de Conquista -->
            <div class="achievements-section">
              <h3>Conquistas 🏆</h3>
              <div class="achievements-grid">
                <div
                  class="achievement-badge"
                  title="7 dias consecutivos de treino"
                >
                  <i class="bx bx-fire"></i>
                  <span>7 Dias</span>
                </div>
                <div class="achievement-badge" title="Meta de treinos atingida">
                  <i class="bx bx-trophy"></i>
                  <span>Meta 75%</span>
                </div>
                <div class="achievement-badge" title="Novo recorde de força">
                  <i class="bx bx-bolt"></i>
                  <span>Novo PR</span>
                </div>
              </div>
            </div>
          </section>

          <!-- ──── CRIAR TREINO ──── -->
          <section
            id="section-criar-treino"
            class="section"
            aria-labelledby="criar-treino-title"
          >
            <div class="section-header">
              <h1 id="criar-treino-title">Sobre Treino</h1>
              <button
                type="button"
                class="btn-primary"
                onclick="openModal('modal-treino')"
              >
                <i class="bx bx-plus"></i> Novo Treino
              </button>
            </div>
            <div class="filters-bar"></div>
            <div class="table-card">
              <table class="data-table" id="treino-table">
                <thead>
                  <tr>
                    <th scope="col">nome do exercicio</th>
                    <th scope="col">grupo muscular</th>
                    <th scope="col">repeticoes</th>
                    <th scope="col">series</th>
                    <th scope="col">carga</th>
                    <th scope="col">acoes</th>
                  </tr>
                </thead>
                <tbody id="treino-tbody"></tbody>
              </table>
              <div class="table-pagination">
                <span id="treinos-count">0 treinos</span>
                <div class="pag-buttons">
                  <button type="button" class="btn-sm" onclick="changePage(-1)">
                    ‹
                  </button>
                  <span id="pag-info">1 / 1</span>
                  <button type="button" class="btn-sm" onclick="changePage(1)">
                    ›
                  </button>
                </div>
              </div>
            </div>
          </section>

          <!-- ──── MEUS TREINOS ──── -->
          <section
            id="section-meus-treinos"
            class="section"
            aria-labelledby="meus-treinos-title"
          >
            <div class="section-header">
              <h1 id="meus-treinos-title">Treinos</h1>
              <p>Visualize e gerencie seus treinos</p>
            </div>

            <!-- Abas de Filtro -->
            <div class="treino-tabs">
              <button
                type="button"
                class="tab-btn active"
                onclick="filterTreinos(this, 'todos')"
              >
                Todos
              </button>
              <button
                type="button"
                class="tab-btn"
                onclick="filterTreinos(this, 'musculacao')"
              >
                <i class="bx bx-dumbbell"></i> Musculação
              </button>
              <button
                type="button"
                class="tab-btn"
                onclick="filterTreinos(this, 'crossfit')"
              >
                <i class="bx bx-bolt"></i> CrossFit
              </button>
              <button
                type="button"
                class="tab-btn"
                onclick="filterTreinos(this, 'fisioterapia')"
              >
                <i class="bx bx-heart"></i> Fisioterapia
              </button>
            </div>

            <!-- Grid de Treinos -->
            <div class="treinos-grid" id="treinos-grid"></div>
          </section>

          <!-- ──── CALCULADORA DE IMC ──── -->
          <section
            id="section-calculadoradeimc"
            class="section"
            aria-labelledby="calculadoradeimc-title"
          >
            <header>
              <h1>⚡ Sistema de Bioimpedncia</h1>
              <p class="subtitle">
                Anlise de Composio Corporal com Injeo de Dependncia
              </p>
            </header>

            <main>
              <!-- Formulrio de Dados -->
              <section class="card"></section>

              <!-- Histrico de Avaliaes -->
              <section class="card">
                <h2>📚 Historico de Avaliações</h2>
                <div id="historyList" class="history-list">
                  <!-- Avaliaes salvas sero inseridas aqui -->
                </div>
              </section>

              <!-- Log de Operaes -->
              <section class="card">
                <h2>🔬 Log de Operações</h2>
                <div id="logList" class="log-list">
                  <!-- Logs sero inseridos aqui -->
                </div>
              </section>
            </main>
            <h2>📋 Dados do Paciente</h2>
            <div id="patientForm">
              <div class="form-row">
                <div class="form-group">
                  <label for="nome">Nome:</label>
                  <input
                    type="text"
                    id="nome"
                    name="nome"
                    required
                    placeholder="Nome completo"
                  />
                </div>
                <div class="form-group">
                  <label for="idade">Idade:</label>
                  <input
                    type="number"
                    id="idade"
                    name="idade"
                    required
                    placeholder="Anos"
                    min="5"
                    max="100"
                  />
                </div>
              </div>

              <div class="form-row">
                <div class="form-group">
                  <label for="genero">Gnero:</label>
                  <select id="genero" name="genero" required>
                    <option value="">Selecione</option>
                    <option value="masculino">Masculino</option>
                    <option value="feminino">Feminino</option>
                  </select>
                </div>
                <div class="form-group">
                  <label for="altura">Altura (cm):</label>
                  <input
                    type="number"
                    id="altura"
                    name="altura"
                    required
                    placeholder="Ex: 175"
                    min="100"
                    max="250"
                  />
                </div>
              </div>

              <div class="form-row">
                <div class="form-group">
                  <label for="peso">Peso (kg):</label>
                  <input
                    type="number"
                    id="peso"
                    name="peso"
                    required
                    placeholder="Ex: 75.5"
                    step="0.1"
                    min="30"
                    max="300"
                  />
                </div>
                <div class="form-group">
                  <label for="impedancia">Impedncia (Ω):</label>
                  <input
                    type="number"
                    id="impedancia"
                    name="impedancia"
                    required
                    placeholder="Ex: 500"
                    step="1"
                    min="200"
                    max="1500"
                  />
                </div>
              </div>

              <button type="submit" class="btn-primary">
                Calcular Bioimpedncia
              </button>
            </div>

            <!-- Resultados -->
            <h2>📊 Resultados da Anlise</h2>
            <div class="results-grid">
              <div class="result-item highlight">
                <div class="result-icon">💧</div>
                <div class="result-content">
                  <span class="result-label">Massa Magra</span>
                  <span class="result-value" id="massaMagra">-- kg</span>
                  <span class="result-percent" id="massaMagraPercent">--%</span>
                </div>
              </div>

              <div class="result-item highlight">
                <div class="result-icon">🔥</div>
                <div class="result-content">
                  <span class="result-label">Massa Gorda</span>
                  <span class="result-value" id="massaGorda">-- kg</span>
                  <span class="result-percent" id="massaGordaPercent">--%</span>
                </div>
              </div>

              <div class="result-item">
                <div class="result-icon">📏</div>
                <div class="result-content">
                  <span class="result-label">IMC</span>
                  <span class="result-value" id="imc">--</span>
                  <span class="result-classification" id="imcClass">--</span>
                </div>
              </div>

              <div class="result-item">
                <div class="result-icon">⚡</div>
                <div class="result-content">
                  <span class="result-label">Taxa Metablica Basal</span>
                  <span class="result-value" id="tmb">-- kcal</span>
                  <span class="result-detail">por dia</span>
                </div>
              </div>

              <div class="result-item">
                <div class="result-icon">💧</div>
                <div class="result-content">
                  <span class="result-label">agua Corporal</span>
                  <span class="result-value" id="agua">-- kg</span>
                  <span class="result-percent" id="aguaPercent">--%</span>
                </div>
              </div>

              <div class="result-item">
                <div class="result-icon">🦴</div>
                <div class="result-content">
                  <span class="result-label">Massa Ossea</span>
                  <span class="result-value" id="massaOssea">-- kg</span>
                  <span class="result-detail">estimada</span>
                </div>
              </div>
            </div>

            <div class="action-buttons">
              <button
                class="btn-secondary"
                onclick="app.controller.limparResultados()"
              >
                🗑️ Limpar Resultados
              </button>
              <button
                class="btn-primary"
                onclick="app.controller.salvarAvaliacao()"
              >
                💾 Salvar Avaliação
              </button>
            </div>
          </section>
          <!-- ──── CONFIGURAÇÕES ──── -->
          <section
            id="section-configuracoes"
            class="section"
            aria-labelledby="config-title"
          >
            <div class="section-header">
              <h1 id="config-title">Configurações</h1>
            </div>
            <div class="config-grid">
              <div class="config-card">
                <h3><i class="bx bx-store"></i> Academia</h3>
                <div class="form-group">
                  <label>Nome da academia</label>
                  <input type="text" value="PowerGym" />
                </div>
                <div class="form-group">
                  <label>Endereço</label>
                  <input
                    type="text"
                    placeholder="Rua Exemplo, 123 — Ribeirão Preto, SP"
                  />
                </div>
                <div class="form-group">
                  <label>Telefone</label>
                  <input type="tel" placeholder="(16) 3333-0000" />
                </div>
                <button type="button" class="btn-primary">
                  Salvar alterações
                </button>
              </div>
              <div class="config-card">
                <h3><i class="bx bx-shield"></i> Segurança</h3>
                <div class="form-group">
                  <label>Senha atual</label>
                  <input type="password" placeholder="••••••••" />
                </div>
                <div class="form-group">
                  <label>Nova senha</label>
                  <input type="password" placeholder="••••••••" />
                </div>
                <div class="form-group">
                  <label>Confirmar nova senha</label>
                  <input type="password" placeholder="••••••••" />
                </div>
                <div class="form-group toggle-row">
                  <label>Autenticação em dois fatores</label>
                  <label class="toggle">
                    <input type="checkbox" id="2fa-toggle" />
                    <span class="toggle-track"></span>
                  </label>
                </div>
                <button type="button" class="btn-primary">
                  Atualizar senha
                </button>
              </div>
              <div class="config-card">
                <h3><i class="bx bx-bell"></i> Notificações</h3>
                <div class="notif-opts">
                  <div class="form-group toggle-row">
                    <label>Avisar vencimento de mensalidade</label>
                    <label class="toggle">
                      <input type="checkbox" checked />
                      <span class="toggle-track"></span>
                    </label>
                  </div>
                </div>
                <button type="button" class="btn-primary">
                  Salvar preferências
                </button>
              </div>
            </div>
          </section>

          <!-- Modal: Novo Treino (expandido) -->
          <div
            id="modal-treino"
            class="modal"
            role="dialog"
            aria-modal="true"
            aria-hidden="true"
            style="display: none"
          >
            <div class="modal-content">
              <button
                type="button"
                class="modal-close"
                onclick="closeModal('modal-treino')"
                aria-label="Fechar"
              >
                &times;
              </button>
              <h2>Novo Treino</h2>
              <form
                id="form-novo-treino"
                onsubmit="
                  event.preventDefault();
                  submitNovoTreino();
                "
              >
                <div class="form-group">
                  <label for="treino-nome">Nome do treino</label>
                  <input
                    id="treino-nome"
                    name="nome"
                    type="text"
                    placeholder="Ex: Treino A"
                  />
                </div>

                <div class="form-group">
                  <label for="treino-plano">Tipo de Treino</label>
                  <select id="treino-plano" name="tipo">
                    <option value="musculacao">Musculação</option>
                    <option value="crossfit">CrossFit</option>
                    <option value="fisioterapia">Fisioterapia</option>
                  </select>
                </div>

                <div class="form-group">
                  <label for="treino-exercicios"
                    >Exercícios (um por linha)</label
                  >
                  <textarea
                    id="treino-exercicios"
                    name="exercicios"
                    placeholder="Ex:&#10;Supino | 4 | 8&#10;Agachamento | 4 | 10"
                    rows="4"
                  ></textarea>
                  <small style="color: var(--text-muted)"
                    >Formato: Nome do exercício | Séries | Repetições</small
                  >
                </div>

                <div class="form-group">
                  <label for="treino-obs">Observações</label>
                  <textarea
                    id="treino-obs"
                    name="obs"
                    placeholder="Anotações importantes sobre o treino"
                    rows="2"
                  ></textarea>
                </div>

                <div class="form-actions">
                  <button
                    type="button"
                    class="btn-sm"
                    onclick="closeModal('modal-treino')"
                  >
                    Cancelar
                  </button>
                  <button type="submit" class="btn-primary">
                    Salvar Treino
                  </button>
                </div>
              </form>
            </div>
          </div>

          <!-- Modal: Executar Treino (timer + progresso) -->
          <div
            id="modal-execucao"
            class="modal"
            role="dialog"
            aria-modal="true"
            aria-hidden="true"
            style="display: none"
          >
            <div class="modal-content modal-execucao-content">
              <button
                type="button"
                class="modal-close"
                onclick="closeModal('modal-execucao')"
                aria-label="Fechar"
              >
                &times;
              </button>

              <div class="exec-header">
                <h2 id="exec-nome-treino">Treino</h2>
                <div class="exec-progress">
                  <div
                    class="exec-progress-bar"
                    id="exec-progress-bar"
                    style="width: 0%"
                  ></div>
                </div>
                <small
                  id="exec-progresso-texto"
                  style="color: var(--text-muted)"
                  >Exercício 1 de X</small
                >
              </div>

              <div class="exec-body">
                <div id="exec-exercicio-info" class="exec-exercicio-info">
                  <!-- Renderizado por JavaScript -->
                </div>
              </div>

              <div class="exec-actions">
                <button
                  type="button"
                  class="btn-sm"
                  id="btn-pausar-treino"
                  onclick="pausarTreino()"
                >
                  ⏸ Pausar
                </button>
                <button
                  type="button"
                  class="btn-primary-sm"
                  onclick="proximoExercicio()"
                >
                  ✓ Próximo
                </button>
                <button
                  type="button"
                  class="btn-sm danger"
                  onclick="finalizarTreino()"
                >
                  Finalizar Treino
                </button>
              </div>
            </div>
          </div>
        </main>
      </div>
    </div>

    <!-- Carrega as funções de navegação e interação do painel. -->
    <script src="app.js"></script>
  </body>
</html>


/* ═══════════════════════════════════════════════════
   POWERGYM — APP.JS
   Arquitetura: State → Render → Events
   Preparado para substituição por chamadas de API reais
═══════════════════════════════════════════════════ */

// Atalho para localizar elementos pelo ID usado pelas funções da página.
const $ = (id) => document.getElementById(id);

// Mantém a seção aberta e o filtro atual dos treinos.
const State = {
  currentSection: "dashboard",
  treinos: { filter: "todos" },
  execucao: {
    ativo: false,
    treinoId: null,
    treinoNome: "",
    exercicioAtual: 0,
    seriesAtual: 0,
    tempoInicio: null,
    tempoTotal: 0,
    pausado: false,
  },
};

/* ─────────────────────────────────────────
   CAMADA DE DADOS (mock — substituir por fetch/axios)
   Cada função aqui será trocada por uma chamada REST.
   Ex: getAlunos() → fetch('/api/alunos').then(r => r.json())
───────────────────────────────────────── */

const DB = {
  nextId: {
    alunos: 10,
    treinos: 10,
    pagamentos: 10,
  },
  alunos: [
    {
      id: 1,
      nome: "João Silva",
      email: "joao@email.com",
      plano: "Gold",
      status: "Ativo",
    },
    {
      id: 2,
      nome: "Maria Santos",
      email: "maria@email.com",
      plano: "Silver",
      status: "Ativo",
    },
    {
      id: 3,
      nome: "Pedro Costa",
      email: "pedro@email.com",
      plano: "Bronze",
      status: "Inativo",
    },
    {
      id: 4,
      nome: "Ana Oliveira",
      email: "ana@email.com",
      plano: "Gold",
      status: "Ativo",
    },
    {
      id: 5,
      nome: "Lucas Mendes",
      email: "lucas@email.com",
      plano: "Silver",
      status: "Ativo",
    },
  ],
  aluno: [
    {
      id: 1,
      nome: "João Silva",
      email: "joao@email.com",
      plano: "Gold",
      status: "Ativo",
    },
    {
      id: 2,
      nome: "Maria Santos",
      email: "maria@email.com",
      plano: "Silver",
      status: "Ativo",
    },
  ],
  pagamentos: [
    { id: 1, alunoId: 1, valor: 150, status: "Pago" },
    { id: 2, alunoId: 2, valor: 100, status: "Pago" },
  ],
  treinos: [
    {
      id: 1,
      nome: "Treino A",
      tipo: "musculacao",
      alunoId: 1,
      exercicios: [
        ["Supino", "4", "8"],
        ["Agachamento", "4", "10"],
      ],
      obs: "Treino para peito e perna",
      compartilhado: false,
    },
    {
      id: 2,
      nome: "Treino B",
      tipo: "musculacao",
      alunoId: 2,
      exercicios: [
        ["Rosca Direta", "3", "12"],
        ["Barra", "3", "10"],
      ],
      obs: "Treino para braço",
      compartilhado: false,
    },
    {
      id: 3,
      nome: "Supino & Costas",
      tipo: "musculacao",
      alunoId: 1,
      exercicios: [
        ["Supino Declinado", "4", "6"],
        ["Barra Fixa", "4", "8"],
        ["Remada Alta", "3", "10"],
      ],
      obs: "Foco em força e hipertrofia",
      compartilhado: false,
    },
    {
      id: 4,
      nome: "WOD Classe",
      tipo: "crossfit",
      alunoId: 1,
      exercicios: [
        ["Burpee", "3", "15"],
        ["Kettlebell Swing", "3", "20"],
        ["Box Jump", "3", "10"],
      ],
      obs: "Workout Of The Day - Alta intensidade",
      compartilhado: true,
    },
    {
      id: 5,
      nome: "CrossFit Força",
      tipo: "crossfit",
      alunoId: 2,
      exercicios: [
        ["Snatch", "5", "3"],
        ["Clean & Jerk", "5", "2"],
        ["Front Squat", "3", "5"],
      ],
      obs: "Movimentos olímpicos - Força máxima",
      compartilhado: false,
    },
    {
      id: 6,
      nome: "Reabilitação Ombro",
      tipo: "fisioterapia",
      alunoId: 1,
      exercicios: [
        ["Rotação Externa", "3", "15"],
        ["Pendulo Passivo", "3", "20"],
        ["Alongamento Ombro", "3", "30s"],
      ],
      obs: "Recuperação pós-lesão - Baixa carga",
      compartilhado: true,
    },
    {
      id: 7,
      nome: "Fortalecimento Joelho",
      tipo: "fisioterapia",
      alunoId: 2,
      exercicios: [
        ["Mini Agachamento", "3", "10"],
        ["Elevação Perna Deitado", "3", "15"],
        ["Alongamento Isquiotibial", "3", "45s"],
      ],
      obs: "Estabilização e mobilidade",
      compartilhado: false,
    },
  ],
  progresso: {
    pesoAtual: 82.5,
    pesoInicial: 92.0,
    alturaAtual: 1.75,
    imcAtual: 26.9,
    imcMeta: 24.0,
    metaTreinosMes: 24,
    treinosRealizados: 18,
    frequenciaMedia: 4.5,
    diasConsecutivos: 7,
    ganhoForca: 22.5,
  },
  historicoTreinos: [
    {
      id: 1,
      nome: "Supino",
      data: "2026-09-10",
      series: 4,
      reps: 8,
      carga: 80,
      tempo: 45,
    },
    {
      id: 2,
      nome: "Agachamento",
      data: "2026-09-10",
      series: 4,
      reps: 10,
      carga: 120,
      tempo: 40,
    },
    {
      id: 3,
      nome: "Rosca Direta",
      data: "2026-09-09",
      series: 3,
      reps: 12,
      carga: 30,
      tempo: 35,
    },
    {
      id: 4,
      nome: "Barra",
      data: "2026-09-09",
      series: 3,
      reps: 10,
      carga: 50,
      tempo: 38,
    },
    {
      id: 5,
      nome: "Leg Press",
      data: "2026-09-08",
      series: 4,
      reps: 12,
      carga: 180,
      tempo: 42,
    },
    {
      id: 6,
      nome: "Supino",
      data: "2026-09-08",
      series: 4,
      reps: 8,
      carga: 78,
      tempo: 44,
    },
  ],
  historicoMedicoes: [
    { data: "2026-09-01", peso: 90.0, imc: 29.4 },
    { data: "2026-09-08", peso: 86.5, imc: 28.2 },
    { data: "2026-09-10", peso: 82.5, imc: 26.9 },
  ],
};

/* ─────────────────────────────────────────
   NAVEGAÇÃO ENTRE PÁGINAS (Login / Cadastro / Aluno)
───────────────────────────────────────── */
function navigate(page) {
  document
    .querySelectorAll(".page")
    .forEach((p) => p.classList.remove("active"));
  const target = $(`page-${page}`);
  if (target) target.classList.add("active");
  document.body.setAttribute("data-page", page);
}

function doLogin() {
  const email = $("login-email").value.trim();
  const pass = $("login-pass").value;
  const err = $("login-error");

  if (!email || !pass) {
    err.textContent = "Preencha e-mail e senha.";
    return;
  }
  // TODO: substituir por fetch('/api/auth/login', { method:'POST', body: JSON.stringify({email,pass}) })
  if (email === "aluno@powergym.com" && pass === "123456") {
    err.textContent = "";
    navigate("aluno");
    renderDashboard("");
    renderCriarTreino("");
    renderTreinos("treinos");
    renderConfigurações("configuracoes");
    $("today-date").textContent = new Date().toLocaleDateString("pt-BR", {
      weekday: "long",
      day: "numeric",
      month: "long",
      year: "numeric",
    });
  } else {
    err.textContent =
      "Credenciais inválidas. Tente aluno@powergym.com / 123456";
    $("login-pass").value = "";
  }
}

function doLogout() {
  navigate("login");
  $("login-email").value = "";
  $("login-pass").value = "";
  $("login-error").textContent = "";
}

function doRegistro() {
  const nome = $("reg-nome").value.trim();
  const email = $("reg-email").value.trim();
  const pass = $("reg-pass").value;
  const plano = $("reg-plano").value;
  if (!nome || !email || !pass || !plano) {
    showToast("Preencha todos os campos obrigatórios.", "error");
    return;
  }
  // TODO: fetch('/api/auth/registro', { method:'POST', body: ... })
  showToast(`Conta criada para ${nome}!`, "success");
  navigate("login");
}

function togglePass() {
  const input = $("login-pass");
  const icon = $("pass-icon");
  if (input.type === "password") {
    input.type = "text";
    icon.className = "bx bx-hide";
  } else {
    input.type = "password";
    icon.className = "bx bx-show";
  }
}

/* ─────────────────────────────────────────
   NAVEGAÇÃO DE SEÇÕES (dentro do Aluno)
───────────────────────────────────────── */
function showSection(btn, section) {
  // Remove o destaque e oculta todas as seções antes de ativar a escolhida.
  document
    .querySelectorAll(".nav-item")
    .forEach((n) => n.classList.remove("active"));
  document
    .querySelectorAll(".section")
    .forEach((s) => s.classList.remove("active"));
  if (btn) btn.classList.add("active");
  const sec = $(`section-${section}`);
  if (sec) sec.classList.add("active");

  // Salva a seção atual para que outras ações possam reutilizá-la.
  State.currentSection = section;
  const labels = {
    dashboard: "Dashboard",
    progresso: "Meu Progresso",
    "criar-treino": "Criar Treino",
    "meus-treinos": "Meus Treinos",
    calculadoradeimc: "Calculadora de IMC",
    configuracoes: "Configurações",
  };
  // Atualiza o título exibido no topo do painel.
  $("breadcrumb").textContent = labels[section] || section;

  // Renderizar dados específicos de cada seção
  if (section === "progresso") {
    renderProgresso();
  }
  if (section === "meus-treinos") {
    State.treinos.filter = "todos";
    renderTreinos();
  }

  // Fecha a barra lateral depois da seleção em telas pequenas.
  document.getElementById("sidebar").classList.remove("open");
}

function toggleSidebar() {
  const sb = $("sidebar");
  if (window.innerWidth <= 768) {
    sb.classList.toggle("open");
  } else {
    sb.classList.toggle("collapsed");
  }
}

/* ─────────────────────────────────────────
   DASHBOARD
───────────────────────────────────────── */
function renderDashboard() {
  const ativos = DB.alunos.filter((a) => a.status === "Ativo").length;
  const pagas = DB.pagamentos.filter((p) => p.status === "Pago").length;
  const kpiAluno = $("kpi-aluno");
  const kpiPagas = $("kpi-pagas");
  if (kpiAluno) kpiAluno.textContent = ativos;
  if (kpiPagas) kpiPagas.textContent = pagas;

  const tbody = $("dash-treinos-tbody");
  if (!tbody) return;

  const rows = DB.treinos
    .slice(0, 5)
    .map(
      (t) => `
    <tr>
      <td>${t.nome}</td>
      <td>${t.tipo}</td>
      <td><span class="badge-status active">Ativo</span></td>
      <td>
        <div class="row-actions">
          <button class="btn-icon" onclick="editTreino(${t.id})" title="Editar"><i class='bx bx-edit'></i></button>
        </div>
      </td>
    </tr>
  `,
    )
    .join("");
  tbody.innerHTML = rows;
}

/* ─────────────────────────────────────────
MEU PROGRESSO
───────────────────────────────────────── */
function renderProgresso() {
  const prog = DB.progresso;

  // Atualizar KPIs
  const pesoPerdido = (prog.pesoInicial - prog.pesoAtual).toFixed(1);
  const percentualPeso = ((pesoPerdido / prog.pesoInicial) * 100).toFixed(1);

  const elem = (id) => $(id);
  if (elem("progress-peso-perdido"))
    elem("progress-peso-perdido").textContent = `${pesoPerdido} kg`;
  if (elem("progress-imc"))
    elem("progress-imc").textContent = prog.imcAtual.toFixed(1);
  if (elem("progress-treinos"))
    elem("progress-treinos").textContent =
      `${prog.treinosRealizados} / ${prog.metaTreinosMes}`;
  if (elem("progress-forca"))
    elem("progress-forca").textContent = `+${prog.ganhoForca}%`;

  // Renderizar gráfico de peso
  renderGraficoPeso();

  // Renderizar histórico de treinos
  renderHistoricoTreinos();
}

function renderGraficoPeso() {
  const historico = DB.historicoMedicoes;
  const container = $("chart-peso");
  if (!container) return;

  const maxPeso = Math.max(...historico.map((h) => h.peso));
  const minPeso = Math.min(...historico.map((h) => h.peso));
  const range = maxPeso - minPeso;

  const html = historico
    .map((h, idx) => {
      const altura = ((h.peso - minPeso) / range) * 150;
      const data = new Date(h.data).toLocaleDateString("pt-BR", {
        day: "2-digit",
        month: "short",
      });
      return `
        <div class="bar-item" title="${h.peso} kg">
          <div class="bar" style="height: ${altura}px"></div>
          <div class="bar-label">${data}</div>
          <div class="bar-value">${h.peso} kg</div>
        </div>
      `;
    })
    .join("");

  container.innerHTML = html;
}

function renderHistoricoTreinos() {
  const tbody = $("historico-treinos-tbody");
  if (!tbody) return;

  const rows = DB.historicoTreinos
    .map(
      (t) => `
    <tr>
      <td>${t.nome}</td>
      <td>${new Date(t.data).toLocaleDateString("pt-BR")}</td>
      <td>${t.series} × ${t.reps}</td>
      <td>${t.carga} kg</td>
      <td>${t.tempo} min</td>
    </tr>
  `,
    )
    .join("");

  tbody.innerHTML = rows;
}

/* ─────────────────────────────────────────
CRIAR TREINOS
───────────────────────────────────────── */

/* ─────────────────────────────────────────
MEUS TREINOS
───────────────────────────────────────── */
function filterTreinos(btn, tipo) {
  document
    .querySelectorAll(".tab-btn")
    .forEach((b) => b.classList.remove("active"));
  btn.classList.add("active");
  State.treinos.filter = tipo;
  renderTreinos();
}

function renderTreinos() {
  const filtro = State.treinos.filter;
  const lista =
    filtro === "todos"
      ? DB.treinos
      : DB.treinos.filter((t) => t.tipo === filtro);
  const grid = $("treinos-grid");

  if (!lista.length) {
    grid.innerHTML = `<div class="empty-state" style="grid-column:1/-1"><i class='bx bx-run'></i><p>Nenhum treino nesta categoria</p></div>`;
    return;
  }

  const typeLabels = {
    musculacao: "Musculação",
    crossfit: "CrossFit",
    fisioterapia: "Fisioterapia",
  };

  const typeIcons = {
    musculacao: "bx-dumbbell",
    crossfit: "bx-bolt",
    fisioterapia: "bx-heart",
  };

  grid.innerHTML = lista
    .map(
      (t) => `
    <div class="treino-card">
      <div class="treino-card-header">
        <div>
          <h3>${t.nome}</h3>
          <span class="treino-type-badge ${t.tipo}">
            <i class="bx ${typeIcons[t.tipo]}"></i> ${typeLabels[t.tipo]}
          </span>
          ${t.compartilhado ? '<span class="badge-compartilhado"><i class="bx bx-share"></i> Compartilhado</span>' : ""}
        </div>
        <div class="treino-actions">
          <button class="btn-icon-sm" onclick="compartilharTreino(${t.id})" title="${t.compartilhado ? "Remover compartilhamento" : "Compartilhar"}"><i class='bx ${t.compartilhado ? "bx-share-alt" : "bx-share"}'></i></button>
          <button class="btn-icon-sm" onclick="duplicarTreino(${t.id})" title="Duplicar"><i class='bx bx-copy'></i></button>
          <button class="btn-icon-sm" onclick="editTreino(${t.id})" title="Editar"><i class='bx bx-edit'></i></button>
          <button class="btn-icon-sm danger" onclick="deleteTreino(${t.id})" title="Excluir"><i class='bx bx-trash'></i></button>
        </div>
      </div>
      
      <div class="treino-card-body">
        ${t.obs ? `<p class="treino-obs"><i class='bx bx-info-circle'></i> ${t.obs}</p>` : ""}
        
        <div class="treino-exercicios">
          <h4>Exercícios (${t.exercicios.length})</h4>
          <table>
            <thead>
              <tr>
                <th>Exercício</th>
                <th>Séries</th>
                <th>Reps</th>
              </tr>
            </thead>
            <tbody>
              ${t.exercicios.map((e) => `<tr><td>${e[0]}</td><td>${e[1]}</td><td>${e[2]}</td></tr>`).join("")}
            </tbody>
          </table>
        </div>
      </div>
      
      <div class="treino-card-footer">
        <button class="btn-primary-sm" onclick="iniciarTreino(${t.id})">
          <i class='bx bx-play'></i> Iniciar Treino
        </button>
      </div>
    </div>
  `,
    )
    .join("");
}

function saveTreino() {
  const nome = $("t-nome").value.trim();
  const tipo = $("t-tipo").value;
  const alunoId = parseInt($("t-aluno").value);
  const raw = $("t-exercicios").value.trim();
  if (!nome || !raw) {
    showToast("Preencha nome e exercícios.", "error");
    return;
  }

  const exercicios = raw
    .split("\n")
    .map((l) => l.split("|").map((s) => s.trim()))
    .filter((l) => l.length >= 2);
  const obs = $("t-obs").value.trim();

  // TODO: fetch('/api/treinos', { method:'POST', body: JSON.stringify({...}) })
  DB.treinos.push({
    id: DB.nextId.treinos++,
    nome,
    tipo,
    alunoId,
    exercicios,
    obs,
  });
  showToast("Treino criado!");
  closeModal("modal-treino");
  ["t-nome", "t-exercicios", "t-obs"].forEach((id) => ($(id).value = ""));
  renderTreinos();
}

function deleteTreino(id) {
  if (!confirm("Remover este treino?")) return;
  // TODO: fetch(`/api/treinos/${id}`, { method:'DELETE' })
  DB.treinos = DB.treinos.filter((t) => t.id !== id);
  showToast("Treino removido.", "info");
  renderTreinos();
}

function duplicarTreino(id) {
  const treino = DB.treinos.find((t) => t.id === id);
  if (!treino) return;

  const novoTreino = {
    id: DB.nextId.treinos++,
    nome: `${treino.nome} (cópia)`,
    tipo: treino.tipo,
    alunoId: treino.alunoId,
    exercicios: treino.exercicios.map((e) => [...e]),
    obs: treino.obs,
  };

  DB.treinos.push(novoTreino);
  showToast("Treino duplicado!", "success");
  renderTreinos();
}

function iniciarTreino(id) {
  const treino = DB.treinos.find((t) => t.id === id);
  if (!treino) return;

  // Inicia execução do treino
  State.execucao = {
    ativo: true,
    treinoId: id,
    treinoNome: treino.nome,
    exercicioAtual: 0,
    seriesAtual: 0,
    tempoInicio: Date.now(),
    tempoTotal: 0,
    pausado: false,
  };

  // Mostrar modal de execução
  openModal("modal-execucao");
  renderExecucaoTreino();
  showToast(`Treino "${treino.nome}" iniciado! 💪`, "success");
}

function renderExecucaoTreino() {
  const exec = State.execucao;
  if (!exec.ativo) return;

  const treino = DB.treinos.find((t) => t.id === exec.treinoId);
  if (!treino) return;

  const exercicioAtual = treino.exercicios[exec.exercicioAtual];
  if (!exercicioAtual) {
    finalizarTreino();
    return;
  }

  const nome = $("exec-nome-treino");
  if (nome) nome.textContent = exec.treinoNome;

  // Progressbar
  const progresso = $("exec-progress-bar");
  if (progresso) {
    const percent =
      ((exec.exercicioAtual + 1) / treino.exercicios.length) * 100;
    progresso.style.width = percent + "%";
  }

  // Exercício atual
  const exInfo = $("exec-exercicio-info");
  if (exInfo) {
    const tempoExercicio = Math.floor(
      (Date.now() - State.execucao.tempoInicio) / 1000,
    );
    exInfo.innerHTML = `
      <h2>${exercicioAtual[0]}</h2>
      <div class="exec-detalhes">
        <div class="detalhe">
          <span class="label">Séries</span>
          <span class="valor">${exec.seriesAtual + 1} / ${exercicioAtual[1]}</span>
        </div>
        <div class="detalhe">
          <span class="label">Reps</span>
          <span class="valor">${exercicioAtual[2]} reps</span>
        </div>
        <div class="detalhe">
          <span class="label">Tempo</span>
          <span class="valor" id="exec-tempo">${tempoExercicio}s</span>
        </div>
      </div>
    `;
  }

  // Indicador de progressão
  const progressoTexto = $("exec-progresso-texto");
  if (progressoTexto) {
    progressoTexto.textContent = `Exercício ${exec.exercicioAtual + 1} de ${treino.exercicios.length}`;
  }

  // Atualizar timer a cada segundo
  if (!exec.pausado) {
    setTimeout(renderExecucaoTreino, 1000);
  }
}

function proximoExercicio() {
  const treino = DB.treinos.find((t) => t.id === State.execucao.treinoId);
  if (!treino) return;

  const exercicioAtual = treino.exercicios[State.execucao.exercicioAtual];
  const series = parseInt(exercicioAtual[1]);

  // Incrementar série
  if (State.execucao.seriesAtual < series - 1) {
    State.execucao.seriesAtual++;
    showToast(`✓ Série ${State.execucao.seriesAtual + 1} pronta!`, "success");
  } else {
    // Ir para próximo exercício
    State.execucao.seriesAtual = 0;
    State.execucao.exercicioAtual++;
    showToast(`✓ Exercício concluído! Próximo...`, "info");
  }

  renderExecucaoTreino();
}

function pausarTreino() {
  State.execucao.pausado = !State.execucao.pausado;
  const btn = $("btn-pausar-treino");
  if (btn) {
    btn.textContent = State.execucao.pausado ? "▶ Retomar" : "⏸ Pausar";
  }
  if (!State.execucao.pausado) {
    State.execucao.tempoInicio = Date.now() - State.execucao.tempoTotal;
    renderExecucaoTreino();
  }
}

function finalizarTreino() {
  const exec = State.execucao;
  const tempoTotal = Math.floor((Date.now() - exec.tempoInicio) / 1000);
  const treino = DB.treinos.find((t) => t.id === exec.treinoId);

  if (treino) {
    // Adicionar ao histórico
    treino.exercicios.forEach((ex, idx) => {
      DB.historicoTreinos.unshift({
        id: DB.historicoTreinos.length + 1,
        nome: ex[0],
        data: new Date().toISOString().split("T")[0],
        series: parseInt(ex[1]),
        reps: parseInt(ex[2]),
        carga: 0, // TODO: registrar carga real durante execução
        tempo: Math.ceil(tempoTotal / treino.exercicios.length),
      });
    });

    // Atualizar progresso
    DB.progresso.treinosRealizados++;
    DB.progresso.diasConsecutivos = Math.min(
      DB.progresso.diasConsecutivos + 1,
      365,
    );
  }

  showToast(
    `🎉 Treino "${exec.treinoNome}" finalizado! ${tempoTotal}s de dedicação!`,
    "success",
  );

  State.execucao.ativo = false;
  closeModal("modal-execucao");
  renderProgresso();
  renderTreinos();
}

function compartilharTreino(id) {
  const treino = DB.treinos.find((t) => t.id === id);
  if (!treino) return;

  treino.compartilhado = !treino.compartilhado;
  showToast(
    treino.compartilhado
      ? `Treino compartilhado com outros alunos! 🤝`
      : `Treino deixou de ser compartilhado.`,
    treino.compartilhado ? "success" : "info",
  );
  renderTreinos();
}

function copiarTreinoCompartilhado(id) {
  const treinoOrigem = DB.treinos.find((t) => t.id === id);
  if (!treinoOrigem) return;

  const novoCopia = {
    id: DB.nextId.treinos++,
    nome: `${treinoOrigem.nome} (minha cópia)`,
    tipo: treinoOrigem.tipo,
    alunoId: 1, // Assumir aluno logado
    exercicios: treinoOrigem.exercicios.map((e) => [...e]),
    obs: treinoOrigem.obs,
    compartilhado: false,
  };

  DB.treinos.push(novoCopia);
  showToast(
    `Treino "${treinoOrigem.nome}" adicionado aos seus treinos! 📋`,
    "success",
  );
  renderTreinos();
}

/* ─────────────────────────────────────────
CALCULADORA DE IMC
───────────────────────────────────────── */
// ============================================
// CAMADA DE DEPENDNCIAS (INFRAESTRUTURA)
// ============================================

/**
 * LoggerService - Servio de log
 */
class LoggerService {
  constructor(prefix = "[BIO]") {
    this.prefix = prefix;
    this.logs = [];
  }

  info(message) {
    const timestamp = new Date().toLocaleTimeString("pt-BR");
    const log = { type: "info", timestamp, message };
    this.logs.push(log);
    console.log(`${this.prefix} [INFO] [${timestamp}] ${message}`);
    return log;
  }

  success(message) {
    const timestamp = new Date().toLocaleTimeString("pt-BR");
    const log = { type: "success", timestamp, message };
    this.logs.push(log);
    console.log(`${this.prefix} [SUCCESS] [${timestamp}] ${message}`);
    return log;
  }

  error(message) {
    const timestamp = new Date().toLocaleTimeString("pt-BR");
    const log = { type: "error", timestamp, message };
    this.logs.push(log);
    console.error(`${this.prefix} [ERROR] [${timestamp}] ${message}`);
    return log;
  }

  getLogs() {
    return this.logs;
  }
}

/**
 * StorageRepository - Repositrio de armazenamento
 */
class StorageRepository {
  constructor(storage = localStorage, logger) {
    this.storage = storage;
    this.logger = logger;
    this.avaliacoesKey = "bioimpedancia_avaliacoes";
  }

  getAllAvaliacoes() {
    try {
      const data = this.storage.getItem(this.avaliacoesKey);
      const avaliacoes = data ? JSON.parse(data) : [];
      this.logger.info(`Buscou ${avaliacoes.length} avaliaes do storage`);
      return avaliacoes;
    } catch (error) {
      this.logger.error(`Erro ao buscar avaliaes: ${error.message}`);
      return [];
    }
  }

  saveAvaliacao(avaliacao) {
    try {
      const avaliacoes = this.getAllAvaliacoes();
      avaliacao.id = Date.now();
      avaliacao.dataCriacao = new Date().toISOString();
      avaliacoes.unshift(avaliacao); // Adiciona no incio
      this.storage.setItem(this.avaliacoesKey, JSON.stringify(avaliacoes));
      this.logger.success(`Avaliao salva: ${avaliacao.paciente.nome}`);
      return avaliacao;
    } catch (error) {
      this.logger.error(`Erro ao salvar avaliao: ${error.message}`);
      return null;
    }
  }

  deleteAvaliacao(id) {
    try {
      const avaliacoes = this.getAllAvaliacoes();
      const filtered = avaliacoes.filter((a) => a.id !== id);
      if (filtered.length < avaliacoes.length) {
        this.storage.setItem(this.avaliacoesKey, JSON.stringify(filtered));
        this.logger.success(`Avaliao removida: ID ${id}`);
        return true;
      }
      this.logger.error(`Avaliao no encontrada: ID ${id}`);
      return false;
    } catch (error) {
      this.logger.error(`Erro ao remover avaliao: ${error.message}`);
      return false;
    }
  }
}

// ============================================
// CAMADA DE CLCULO (FRMULAS DE BIOIMPEDNCIA)
// ============================================

/**
 * BioimpedanciaCalculator - Calculadora de bioimpedncia
 * Implementa frmulas baseadas em equaes cientficas
 */
class BioimpedanciaCalculator {
  constructor(logger) {
    this.logger = logger;
    this.logger.info("BioimpedanciaCalculator inicializado");
  }

  /**
   * Calcula a Massa Magra (FFM - Fat Free Mass)
   * Frmula de Kushner (1992) - uma das mais utilizadas
   * FFM = (0.734 * (altura^2 / impedncia)) + (0.116 * peso) + (0.096 * altura) + (0.878 * sexo) - 4.03
   * Onde: sexo = 1 para masculino, 0 para feminino
   */
  calcularMassaMagra(peso, altura, impedancia, genero) {
    const alturaM = altura / 100; // Converte para metros
    const sexo = genero === "masculino" ? 1 : 0;

    // Equao de Kushner adaptada
    const ffm =
      0.734 * (Math.pow(alturaM, 2) / (impedancia / 1000)) +
      0.116 * peso +
      0.096 * alturaM * 100 +
      0.878 * sexo * 10 -
      4.03;

    // Ajuste para valores realistas
    const massaMagraAjustada = Math.max(ffm * 0.85, peso * 0.5);

    this.logger.info(
      `Massa magra calculada: ${massaMagraAjustada.toFixed(2)} kg`,
    );
    return Math.min(massaMagraAjustada, peso * 0.95); // Limite mximo 95% do peso
  }

  /**
   * Calcula a Massa Gorda
   * Massa Gorda = Peso Total - Massa Magra
   */
  calcularMassaGorda(peso, massaMagra) {
    const massaGorda = peso - massaMagra;
    this.logger.info(`Massa gorda calculada: ${massaGorda.toFixed(2)} kg`);
    return Math.max(massaGorda, 0);
  }

  /**
   * Calcula o IMC (ndice de Massa Corporal)
   * IMC = peso / altura^2
   */
  calcularIMC(peso, altura) {
    const alturaM = altura / 100;
    const imc = peso / Math.pow(alturaM, 2);
    this.logger.info(`IMC calculado: ${imc.toFixed(2)}`);
    return imc;
  }

  /**
   * Classifica o IMC segundo a OMS
   */
  classificarIMC(imc) {
    if (imc < 18.5) return { classificacao: "Abaixo do peso", cor: "#29b6f6" };
    if (imc < 25) return { classificacao: "Peso normal", cor: "#00c853" };
    if (imc < 30) return { classificacao: "Sobrepeso", cor: "#ff9800" };
    if (imc < 35) return { classificacao: "Obesidade Grau I", cor: "#ff5722" };
    if (imc < 40) return { classificacao: "Obesidade Grau II", cor: "#f44336" };
    return { classificacao: "Obesidade Grau III", cor: "#b71c1c" };
  }

  /**
   * Calcula a Taxa Metablica Basal (TMB)
   * Frmula de Mifflin-St Jeor (1990) - considerada a mais precisa
   */
  calcularTMB(peso, altura, idade, genero) {
    // Mifflin-St Jeor Equation
    let tmb = 10 * peso + 6.25 * altura - 5 * idade;

    if (genero === "masculino") {
      tmb += 5;
    } else {
      tmb -= 161;
    }

    this.logger.info(`TMB calculada: ${tmb.toFixed(2)} kcal/dia`);
    return tmb;
  }

  /**
   * Calcula a gua Corporal Total
   * Aproximao: 73% da massa magra
   */
  calcularAguaCorporal(massaMagra) {
    const agua = massaMagra * 0.73;
    this.logger.info(`gua corporal calculada: ${agua.toFixed(2)} kg`);
    return agua;
  }

  /**
   * Estima a Massa ssea
   * Aproximao: ~5% do peso corporal para adultos
   */
  calcularMassaOssea(peso, genero) {
    // Mulheres tendem a ter menor densidade ssea
    const percentual = genero === "masculino" ? 0.05 : 0.045;
    const massaOssea = peso * percentual;
    this.logger.info(`Massa ssea estimada: ${massaOssea.toFixed(2)} kg`);
    return massaOssea;
  }

  /**
   * Realiza todos os clculos de bioimpedncia
   */
  calcularTodos(paciente, dadosMedicao) {
    this.logger.info(`Iniciando clculos para: ${paciente.nome}`);

    const { peso, altura, idade, genero } = paciente;
    const { impedancia } = dadosMedicao;

    // Calcula massa magra usando frmula de bioimpedncia
    const massaMagra = this.calcularMassaMagra(
      peso,
      altura,
      impedancia,
      genero,
    );

    // Calcula os demais valores
    const massaGorda = this.calcularMassaGorda(peso, massaMagra);
    const imc = this.calcularIMC(peso, altura);
    const imcClassificacao = this.classificarIMC(imc);
    const tmb = this.calcularTMB(peso, altura, idade, genero);
    const agua = this.calcularAguaCorporal(massaMagra);
    const massaOssea = this.calcularMassaOssea(peso, genero);

    // Calcula percentuais
    const percentualGordura = (massaGorda / peso) * 100;
    const percentualMassaMagra = (massaMagra / peso) * 100;
    const percentualAgua = (agua / peso) * 100;

    this.logger.success(`Clculos completados para ${paciente.nome}`);

    return {
      paciente,
      dadosMedicao,
      resultados: {
        massaMagra: parseFloat(massaMagra.toFixed(2)),
        massaMagraPercent: parseFloat(percentualMassaMagra.toFixed(1)),
        massaGorda: parseFloat(massaGorda.toFixed(2)),
        massaGordaPercent: parseFloat(percentualGordura.toFixed(1)),
        imc: parseFloat(imc.toFixed(2)),
        imcClassificacao: imcClassificacao.classificacao,
        imcCor: imcClassificacao.cor,
        tmb: parseFloat(tmb.toFixed(0)),
        agua: parseFloat(agua.toFixed(2)),
        aguaPercent: parseFloat(percentualAgua.toFixed(1)),
        massaOssea: parseFloat(massaOssea.toFixed(2)),
      },
      dataCalculo: new Date().toISOString(),
    };
  }
}

// ============================================
// CAMADA DE SERVIO (BUSINESS LOGIC)
// ============================================

/**
 * BioimpedanciaService - Servio de negcio
 */
class BioimpedanciaService {
  constructor(calculator, repository, logger) {
    this.calculator = calculator;
    this.repository = repository;
    this.logger = logger;
    this.logger.info("BioimpedanciaService inicializado");
  }

  validarDados(paciente, dadosMedicao) {
    this.logger.info("Validando dados do paciente");

    const erros = [];

    // Validaes bsicas
    if (!paciente.nome || paciente.nome.trim().length < 3) {
      erros.push("Nome deve ter pelo menos 3 caracteres");
    }

    if (!paciente.idade || paciente.idade < 5 || paciente.idade > 100) {
      erros.push("Idade deve estar entre 5 e 100 anos");
    }

    if (!["masculino", "feminino"].includes(paciente.genero)) {
      erros.push("Gnero deve ser masculino ou feminino");
    }

    if (!paciente.altura || paciente.altura < 100 || paciente.altura > 250) {
      erros.push("Altura deve estar entre 100 e 250 cm");
    }

    if (!paciente.peso || paciente.peso < 30 || paciente.peso > 300) {
      erros.push("Peso deve estar entre 30 e 300 kg");
    }

    if (
      !dadosMedicao.impedancia ||
      dadosMedicao.impedancia < 200 ||
      dadosMedicao.impedancia > 1500
    ) {
      erros.push("Impedncia deve estar entre 200 e 1500 ohms");
    }

    if (erros.length > 0) {
      this.logger.error(`Validao falhou: ${erros.join(", ")}`);
    }

    return { valido: erros.length === 0, erros };
  }

  calcularBioimpedancia(paciente, dadosMedicao) {
    this.logger.info(`Calculando bioimpedncia para: ${paciente.nome}`);

    const validacao = this.validarDados(paciente, dadosMedicao);
    if (!validacao.valido) {
      throw new Error(validacao.erros.join("; "));
    }

    // Realiza todos os clculos
    const avaliacao = this.calculator.calcularTodos(paciente, dadosMedicao);

    this.logger.success(
      `Bioimpedncia calculada com sucesso para ${paciente.nome}`,
    );
    return avaliacao;
  }

  salvarAvaliacao(avaliacao) {
    this.logger.info("Salvando avaliao");
    return this.repository.saveAvaliacao(avaliacao);
  }

  listarAvaliacoes() {
    this.logger.info("Listando histrico de avaliaes");
    return this.repository.getAllAvaliacoes();
  }

  removerAvaliacao(id) {
    this.logger.info(`Removendo avaliao: ID ${id}`);
    return this.repository.deleteAvaliacao(id);
  }
}

// ============================================
// CONTAINER DE INJEO DE DEPENDNCIA
// ============================================

const Container = {
  services: {},

  register(name, factory) {
    this.services[name] = factory;
    console.log(`[Container] Servio registrado: ${name}`);
  },

  get(name) {
    const factory = this.services[name];
    if (!factory) {
      throw new Error(`Servio "${name}" no registrado no container.`);
    }
    return factory(Container);
  },

  has(name) {
    return name in this.services;
  },
};

// ============================================
// REGISTRO DAS DEPENDNCIAS
// ============================================

Container.register("logger", () => {
  return new LoggerService("[BioApp]");
});

Container.register("repository", (c) => {
  const logger = c.get("logger");
  return new StorageRepository(localStorage, logger);
});

Container.register("calculator", (c) => {
  const logger = c.get("logger");
  return new BioimpedanciaCalculator(logger);
});

Container.register("service", (c) => {
  const calculator = c.get("calculator");
  const repository = c.get("repository");
  const logger = c.get("logger");
  return new BioimpedanciaService(calculator, repository, logger);
});

// ============================================
// CONTROLLER / UI
// ============================================

class BioimpedanciaController {
  constructor(service, logger) {
    this.service = service;
    this.logger = logger;
    this.patientForm = document.getElementById("patientForm");
    this.resultsCard = document.getElementById("resultsCard");
    this.historyList = document.getElementById("historyList");
    this.logList = document.getElementById("logList");
    this.currentAvaliacao = null;

    this.logger.info("BioimpedanciaController inicializado");
    this.init();
  }

  init() {
    this.bindEvents();
    this.renderHistory();
    this.logger.success("Sistema de bioimpedncia inicializado!");
  }

  bindEvents() {
    this.patientForm.addEventListener("submit", (e) =>
      this.handleFormSubmit(e),
    );
  }

  handleFormSubmit(e) {
    e.preventDefault();

    const paciente = {
      nome: document.getElementById("nome").value,
      idade: parseInt(document.getElementById("idade").value),
      genero: document.getElementById("genero").value,
      altura: parseFloat(document.getElementById("altura").value),
      peso: parseFloat(document.getElementById("peso").value),
    };

    const dadosMedicao = {
      impedancia: parseFloat(document.getElementById("impedancia").value),
    };

    try {
      const avaliacao = this.service.calcularBioimpedancia(
        paciente,
        dadosMedicao,
      );
      this.currentAvaliacao = avaliacao;
      this.renderResultados(avaliacao);
      this.resultsCard.style.display = "block";
      this.resultsCard.scrollIntoView({ behavior: "smooth", block: "nearest" });
      this.addLog("Bioimpedncia calculada com sucesso!", "success");
    } catch (error) {
      this.addLog(`Erro: ${error.message}`, "error");
      alert(`Erro: ${error.message}`);
    }
  }

  renderResultados(avaliacao) {
    const { resultados } = avaliacao;

    // Massa Magra
    document.getElementById("massaMagra").textContent =
      `${resultados.massaMagra} kg`;
    document.getElementById("massaMagraPercent").textContent =
      `${resultados.massaMagraPercent}%`;

    // Massa Gorda
    document.getElementById("massaGorda").textContent =
      `${resultados.massaGorda} kg`;
    document.getElementById("massaGordaPercent").textContent =
      `${resultados.massaGordaPercent}%`;

    // IMC
    document.getElementById("imc").textContent = resultados.imc;
    const imcClass = document.getElementById("imcClass");
    imcClass.textContent = resultados.imcClassificacao;
    imcClass.style.color = resultados.imcCor;

    // TMB
    document.getElementById("tmb").textContent = `${resultados.tmb} kcal`;

    // gua
    document.getElementById("agua").textContent = `${resultados.agua} kg`;
    document.getElementById("aguaPercent").textContent =
      `${resultados.aguaPercent}%`;

    // Massa ssea
    document.getElementById("massaOssea").textContent =
      `${resultados.massaOssea} kg`;

    this.logger.info("Resultados renderizados na tela");
  }

  salvarAvaliacao() {
    if (!this.currentAvaliacao) {
      this.addLog("Nenhuma avaliao para salvar", "error");
      return;
    }

    try {
      const salva = this.service.salvarAvaliacao(this.currentAvaliacao);
      if (salva) {
        this.renderHistory();
        this.addLog("Avaliao salva com sucesso!", "success");
        alert("Avaliao salva com sucesso!");
      }
    } catch (error) {
      this.addLog(`Erro ao salvar: ${error.message}`, "error");
    }
  }

  limparResultados() {
    this.resultsCard.style.display = "none";
    this.patientForm.reset();
    this.currentAvaliacao = null;
    this.logger.info("Resultados limpos");
    this.addLog("Formulrio e resultados limpos", "info");
  }

  renderHistory() {
    const avaliacoes = this.service.listarAvaliacoes();

    if (avaliacoes.length === 0) {
      this.historyList.innerHTML = `
                <div class="empty-state">
                    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path>
                        <polyline points="14 2 14 8 20 8"></polyline>
                        <line x1="16" y1="13" x2="8" y2="13"></line>
                        <line x1="16" y1="17" x2="8" y2="17"></line>
                        <polyline points="10 9 9 9 8 9"></polyline>
                    </svg>
                    <p>Nenhuma avaliao salva ainda</p>
                </div>
            `;
      return;
    }

    this.historyList.innerHTML = avaliacoes
      .map((avaliacao) => {
        const data = new Date(avaliacao.dataCriacao).toLocaleDateString(
          "pt-BR",
        );
        const { resultados } = avaliacao;

        return `
                <div class="history-item" onclick="app.controller.carregarAvaliacao(${avaliacao.id})">
                    <div class="history-info">
                        <strong>${this.escapeHtml(avaliacao.paciente.nome)}</strong>
                        <div class="history-details">
                            <span>IMC: ${resultados.imc}</span>
                            <span>Gordura: ${resultados.massaGordaPercent}%</span>
                            <span>Massa Magra: ${resultados.massaMagra}kg</span>
                        </div>
                    </div>
                    <div class="history-actions">
                        <span class="history-date">${data}</span>
                        <button class="btn-icon" onclick="event.stopPropagation(); app.controller.deletarAvaliacao(${avaliacao.id})" title="Excluir">
                            🗑️
                        </button>
                    </div>
                </div>
            `;
      })
      .join("");

    this.logger.info(`Histrico renderizado: ${avaliacoes.length} avaliaes`);
  }

  carregarAvaliacao(id) {
    const avaliacoes = this.service.listarAvaliacoes();
    const avaliacao = avaliacoes.find((a) => a.id === id);

    if (avaliacao) {
      this.currentAvaliacao = avaliacao;
      this.renderResultados(avaliacao);
      this.resultsCard.style.display = "block";
      this.resultsCard.scrollIntoView({ behavior: "smooth" });
      this.addLog(`Avaliao de ${avaliacao.paciente.nome} carregada`, "info");
    }
  }

  deletarAvaliacao(id) {
    if (confirm("Tem certeza que deseja excluir esta avaliao?")) {
      this.service.removerAvaliacao(id);
      this.renderHistory();

      if (this.currentAvaliacao && this.currentAvaliacao.id === id) {
        this.limparResultados();
      }

      this.addLog("Avaliao excluda", "success");
    }
  }

  addLog(message, type = "info") {
    const timestamp = new Date().toLocaleTimeString("pt-BR");
    const logItem = document.createElement("div");
    logItem.className = `log-item ${type}`;
    logItem.innerHTML = `<span class="log-timestamp">[${timestamp}]</span>${message}`;
    this.logList.insertBefore(logItem, this.logList.firstChild);

    while (this.logList.children.length > 50) {
      this.logList.removeChild(this.logList.lastChild);
    }
  }

  escapeHtml(text) {
    const div = document.createElement("div");
    div.textContent = text;
    return div.innerHTML;
  }
}

// ============================================
// INICIALIZAO DA APLICAO
// ============================================

let app;

document.addEventListener("DOMContentLoaded", () => {
  console.log("=================================");
  console.log("Iniciando Sistema de Bioimpedncia...");
  console.log("=================================");

  const service = Container.get("service");
  const logger = Container.get("logger");

  app = {
    service,
    logger,
    controller: new BioimpedanciaController(service, logger),
  };

  console.log("=================================");
  console.log("Sistema pronto!");
  console.log("=================================");
});

// ============================================
// EXEMPLO DE TESTE COM MOCK
// ============================================

function criarAmbienteDeTeste() {
  console.log("\n=== MODO DE TESTE COM MOCK ===");

  const mockLogger = {
    info: (msg) => console.log("[MOCK LOG]", msg),
    success: (msg) => console.log("[MOCK SUCCESS]", msg),
    error: (msg) => console.error("[MOCK ERROR]", msg),
  };

  const mockCalculator = {
    calcularTodos: (paciente, dados) => {
      mockLogger.info(`Mock: calculando para ${paciente.nome}`);
      return {
        paciente,
        dadosMedicao: dados,
        resultados: {
          massaMagra: 60.5,
          massaMagraPercent: 75.0,
          massaGorda: 19.5,
          massaGordaPercent: 25.0,
          imc: 24.5,
          imcClassificacao: "Peso normal",
          imcCor: "#00c853",
          tmb: 1800,
          agua: 44.2,
          aguaPercent: 55.0,
          massaOssea: 3.5,
        },
        dataCalculo: new Date().toISOString(),
      };
    },
  };

  const testService = new BioimpedanciaService(
    mockCalculator,
    {
      saveAvaliacao: (a) => a,
      getAllAvaliacoes: () => [],
      deleteAvaliacao: () => true,
    },
    mockLogger,
  );

  const teste = testService.calcularBioimpedancia(
    { nome: "Teste", idade: 30, genero: "masculino", altura: 175, peso: 80 },
    { impedancia: 500 },
  );

  console.log("Resultado do teste:", teste.resultados);
  console.log("\n=== FIM DO MODO DE TESTE ===\n");
}

// Descomente para testar com mocks
// criarAmbienteDeTeste();

/* ─────────────────────────────────────────
   FUNÇÕES AUXILIARES
───────────────────────────────────────── */
function showToast(msg, type = "info") {
  const container =
    document.getElementById("toast-container") ||
    (() => {
      const div = document.createElement("div");
      div.id = "toast-container";
      div.style.cssText =
        "position:fixed;top:20px;right:20px;z-index:9999;display:flex;flex-direction:column;gap:10px";
      document.body.appendChild(div);
      return div;
    })();

  const toast = document.createElement("div");
  toast.style.cssText = `
    padding: 12px 16px;
    border-radius: var(--radius-md);
    font-size: 0.9rem;
    background: ${type === "success" ? "var(--green)" : type === "error" ? "var(--red)" : "var(--blue)"};
    color: white;
    box-shadow: var(--shadow-card);
    animation: slideIn 0.3s ease;
  `;
  toast.textContent = msg;
  container.appendChild(toast);

  setTimeout(() => {
    toast.style.animation = "slideOut 0.3s ease";
    setTimeout(() => toast.remove(), 300);
  }, 3000);
}

function openModal(id) {
  const modal = $(id);
  if (modal) {
    modal.style.display = "flex";
    modal.classList.add("open");
  }
}

function closeModal(id) {
  const modal = $(id);
  if (modal) {
    modal.style.display = "none";
    modal.classList.remove("open");
  }
}

function nomeInicial(nome) {
  return nome
    ? nome
        .split(" ")
        .map((n) => n[0])
        .join("")
        .toUpperCase()
        .slice(0, 2)
    : "??";
}

function planoClass(plano) {
  const classes = {
    Gold: "gold",
    Silver: "silver",
    Bronze: "bronze",
  };
  return classes[plano] || "bronze";
}

function statusClass(status) {
  return status === "Ativo" ? "active" : "inactive";
}

function renderConfigurações() {
  // Placeholder — implementar conforme necessário
}

function renderCriarTreino() {
  renderTreinoTable();
}

function renderTreinoTable() {
  const tbody = $("treino-tbody");
  if (!tbody) return;

  const rows = DB.treinos
    .map(
      (t) => `
    <tr>
      <td>${t.nome}</td>
      <td>${t.exercicios[0]?.[0] || "-"}</td>
      <td>${t.exercicios[0]?.[2] || "-"}</td>
      <td>${t.exercicios[0]?.[1] || "-"}</td>
      <td>-</td>
      <td>
        <button class="btn-icon" onclick="editTreino(${t.id})" title="Editar"><i class='bx bx-edit'></i></button>
        <button class="btn-icon" onclick="deleteTreino(${t.id})" title="Excluir"><i class='bx bx-trash'></i></button>
      </td>
    </tr>
  `,
    )
    .join("");

  tbody.innerHTML =
    rows ||
    "<tr><td colspan='6' style='text-align:center;color:var(--text-muted)'>Nenhum treino criado</td></tr>";
  const count = $("treinos-count");
  if (count) count.textContent = `${DB.treinos.length} treinos`;
}

function editTreino(id) {
  const treino = DB.treinos.find((t) => t.id === id);
  if (treino) {
    $("treino-nome").value = treino.nome;
    $("treino-plano").value = treino.tipo;
    openModal("modal-treino");
  }
}

function submitNovoTreino() {
  const nome = $("treino-nome").value.trim();
  const tipo = $("treino-plano").value;
  const rawExercicios = $("treino-exercicios").value.trim();
  const obs = $("treino-obs").value.trim();

  if (!nome || !tipo) {
    showToast("Preencha nome e tipo de treino.", "error");
    return;
  }

  // Parse exercícios no formato: "Nome | Séries | Reps"
  const exercicios = rawExercicios
    .split("\n")
    .map((linha) => linha.split("|").map((s) => s.trim()))
    .filter((linha) => linha.length >= 2 && linha[0]);

  DB.treinos.push({
    id: DB.nextId.treinos++,
    nome,
    tipo,
    alunoId: 1,
    exercicios,
    obs,
  });

  showToast("Treino criado com sucesso!", "success");
  closeModal("modal-treino");
  // Limpar formulário
  $("treino-nome").value = "";
  $("treino-plano").value = "musculacao";
  $("treino-exercicios").value = "";
  $("treino-obs").value = "";
  renderCriarTreino();
  renderTreinos();
}

/* ─────────────────────────────────────────
   ATALHOS DE TECLADO
───────────────────────────────────────── */
document.addEventListener("keydown", (e) => {
  if (e.key === "Escape") {
    document
      .querySelectorAll(".modal-overlay.open")
      .forEach((m) => m.classList.remove("open"));
    if (window.innerWidth <= 768)
      document.getElementById("sidebar").classList.remove("open");
  }
  if ((e.ctrlKey || e.metaKey) && e.key === "k") {
    e.preventDefault();
    const search = $("global-search");
    if (search) {
      search.focus();
      search.select();
    }
  }
});

// Fechar modal ao clicar fora
document.querySelectorAll(".modal-overlay").forEach((overlay) => {
  overlay.addEventListener("click", (e) => {
    if (e.target === overlay) overlay.classList.remove("open");
  });
});

/* ─────────────────────────────────────────
   INIT
───────────────────────────────────────── */
document.addEventListener("DOMContentLoaded", () => {
  // A página começa no login.
  // Para dev, descomente a linha abaixo para ir direto ao admin:
  // navigate('aluno'); renderDashboard(); renderAlunos(); renderTreinos(); renderPagamentos(); renderPlanos();
});




:root {
  --bg-void: #0a0a0b;
  --bg-base: #111114;
  --bg-surface: #18181d;
  --bg-elevated: #1f1f26;
  --bg-hover: #26262f;
  --bg-active: #2d2d38;

  --border: rgba(255, 255, 255, 0.07);
  --border-hover: rgba(255, 255, 255, 0.13);
  --border-strong: rgba(255, 255, 255, 0.2);

  --text-primary: #f0f0f4;
  --text-secondary: #9898a8;
  --text-muted: #5a5a6a;
  --text-on-accent: #fff;

  --accent: #ff6b1a;
  --accent-hover: #ff7d35;
  --accent-dim: rgba(255, 107, 26, 0.15);
  --accent-glow: rgba(255, 107, 26, 0.3);

  --green: #22c55e;
  --green-dim: rgba(34, 197, 94, 0.15);
  --amber: #f59e0b;
  --amber-dim: rgba(245, 158, 11, 0.15);
  --red: #ef4444;
  --red-dim: rgba(239, 68, 68, 0.15);
  --blue: #3b82f6;
  --blue-dim: rgba(59, 130, 246, 0.15);

  --sidebar-w: 240px;
  --topbar-h: 60px;
  --radius-sm: 6px;
  --radius-md: 10px;
  --radius-lg: 14px;
  --radius-xl: 20px;

  --font-display: "Syne", sans-serif;
  --font-body: "DM Sans", sans-serif;

  --trans: 0.18s ease;
  --shadow-card: 0 1px 3px rgba(0, 0, 0, 0.4), 0 4px 16px rgba(0, 0, 0, 0.3);
  --shadow-modal: 0 8px 40px rgba(0, 0, 0, 0.7);
}

*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
html {
  font-size: 16px;
}
body {
  font-family: var(--font-body);
  background: var(--bg-void);
  color: var(--text-primary);
  line-height: 1.5;
  min-height: 100vh;
  overflow-x: hidden;
}

.page {
  display: flex;
  width: 100%;
  min-height: 100vh;
}

.main-wrapper {
  flex: 1;
  min-width: 0;
  display: flex;
  flex-direction: column;
}

a {
  color: var(--accent);
  text-decoration: none;
}
button {
  cursor: pointer;
  font-family: inherit;
}
input,
select,
textarea {
  font-family: inherit;
  font-size: 0.9rem;
  color: var(--text-primary);
}
input::placeholder,
textarea::placeholder {
  color: var(--text-muted);
}
select option {
  background: var(--bg-elevated);
}
textarea {
  resize: vertical;
}

/* ═══════════════════════════════════
   ALUNO SHELL
═══════════════════════════════════ */
#page-aluno {
  display: flex;
  flex-direction: row;
  min-height: 100vh;
}
#page-aluno.active {
  display: flex;
}

/* ── Sidebar ── */
.sidebar {
  width: var(--sidebar-w);
  height: 100vh;
  background: var(--bg-surface);
  border-right: 1px solid var(--border);
  display: flex;
  flex-direction: column;
  position: sticky;
  top: 0;
  flex-shrink: 0;
  transition: width var(--trans);
  z-index: 100;
}
.sidebar.collapsed {
  width: 64px;
}
.sidebar.collapsed .logo-text,
.sidebar.collapsed .nav-item span,
.sidebar.collapsed .aluno-name,
.sidebar.collapsed .aluno-role {
  display: none;
}
.sidebar.collapsed .btn-logout {
  margin: 0 auto;
}

.sidebar-logo {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 20px 18px;
  border-bottom: 1px solid var(--border);
}
.logo-text {
  font-family: var(--font-display);
  font-size: 1.1rem;
  font-weight: 800;
  color: var(--accent);
  letter-spacing: -0.02em;
}

.sidebar-nav {
  flex: 1;
  padding: 12px 8px;
  display: flex;
  flex-direction: column;
  gap: 2px;
  overflow-y: auto;
}
.nav-item {
  display: flex;
  align-items: center;
  gap: 10px;
  width: 100%;
  padding: 10px 12px;
  background: none;
  border: none;
  border-radius: var(--radius-md);
  color: var(--text-secondary);
  font-size: 0.875rem;
  font-weight: 500;
  text-align: left;
  transition: all var(--trans);
}

.nav-item i {
  font-size: 18px;
  flex-shrink: 0;
}
.nav-item:hover {
  background: var(--bg-hover);
  color: var(--text-primary);
}
.nav-item.active {
  background: var(--accent-dim);
  color: var(--accent);
  border: 1px solid rgba(255, 107, 26, 0.2);
}

.sidebar-footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px;
  border-top: 1px solid var(--border);
  gap: 8px;
}
.aluno-info {
  display: flex;
  align-items: center;
  gap: 10px;
  overflow: hidden;
}
.aluno-avatar {
  width: 32px;
  height: 32px;
  background: var(--accent-dim);
  border: 1px solid var(--accent-glow);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.7rem;
  font-weight: 700;
  color: var(--accent);
  flex-shrink: 0;
}
.aluno-name {
  font-size: 0.8rem;
  font-weight: 600;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.aluno-role {
  font-size: 0.7rem;
  color: var(--text-muted);
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
.btn-logout {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 30px;
  height: 30px;
  background: none;
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  color: var(--text-muted);
  font-size: 16px;
  flex-shrink: 0;
  transition: all var(--trans);
}
.btn-logout:hover {
  background: var(--red-dim);
  color: var(--red);
  border-color: var(--red);
}

/* ── Topbar ── */
.topbar {
  height: var(--topbar-h);
  background: var(--bg-surface);
  border-bottom: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 24px;
  gap: 16px;
  position: sticky;
  top: 0;
  z-index: 50;
}
.topbar-left {
  display: flex;
  align-items: center;
  gap: 12px;
}
.menu-toggle {
  display: none;
  align-items: center;
  justify-content: center;
  width: 32px;
  height: 32px;
  background: none;
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  color: var(--text-secondary);
  font-size: 18px;
}
.breadcrumb {
  font-family: var(--font-display);
  font-size: 0.95rem;
  font-weight: 600;
  color: var(--text-primary);
}
.topbar-right {
  display: flex;
  align-items: center;
  gap: 10px;
}
.search-box {
  display: flex;
  align-items: center;
  background: var(--bg-elevated);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  padding: 0 12px;
  gap: 8px;
  width: 220px;
  transition: border-color var(--trans);
}
.search-box:focus-within {
  border-color: var(--accent);
}
.search-box i {
  color: var(--text-muted);
  font-size: 16px;
}
.search-box input {
  background: none;
  border: none;
  outline: none;
  padding: 8px 0;
  width: 100%;
}
.icon-btn {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 36px;
  height: 36px;
  background: var(--bg-elevated);
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  color: var(--text-secondary);
  font-size: 18px;
  transition: all var(--trans);
}
.icon-btn:hover {
  background: var(--bg-hover);
  color: var(--text-primary);
}
.icon-btn .badge {
  position: absolute;
  top: 4px;
  right: 4px;
  width: 16px;
  height: 16px;
  background: var(--accent);
  color: #fff;
  font-size: 0.6rem;
  font-weight: 700;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* ── Content ── */
.content {
  flex: 1;
  padding: 28px;
  overflow-y: auto;
}
.section {
  display: none;
}
.section.active {
  display: block;
}

.section-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  margin-bottom: 28px;
  gap: 16px;
}
.section-header h1 {
  font-family: var(--font-display);
  font-size: 1.6rem;
  font-weight: 700;
  letter-spacing: -0.02em;
}
.section-header p {
  color: var(--text-secondary);
  font-size: 0.875rem;
  margin-top: 4px;
}

/* ═══════════════════════════════════
   KPI CARDS
═══════════════════════════════════ */
.kpi-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 16px;
  margin-bottom: 28px;
}
.kpi-grid.four {
  grid-template-columns: repeat(4, 1fr);
}
.kpi-card {
  background: var(--bg-surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 20px;
  display: flex;
  gap: 16px;
  align-items: center;
  transition:
    border-color var(--trans),
    transform var(--trans);
  box-shadow: var(--shadow-card);
}
.kpi-card:hover {
  border-color: var(--border-hover);
  transform: translateY(-1px);
}
.kpi-card.sm {
  padding: 14px 16px;
  gap: 12px;
}
.kpi-icon {
  width: 48px;
  height: 48px;
  border-radius: var(--radius-md);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 22px;
  flex-shrink: 0;
}
.kpi-icon.sm {
  width: 36px;
  height: 36px;
  font-size: 18px;
}
.kpi-icon.orange {
  background: var(--accent-dim);
  color: var(--accent);
}
.kpi-icon.green {
  background: var(--green-dim);
  color: var(--green);
}
.kpi-icon.blue {
  background: var(--blue-dim);
  color: var(--blue);
}
.kpi-icon.amber {
  background: var(--amber-dim);
  color: var(--amber);
}
.kpi-icon.red {
  background: var(--red-dim);
  color: var(--red);
}
.kpi-label {
  font-size: 0.75rem;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.05em;
  font-weight: 500;
  margin-bottom: 4px;
}
.kpi-value {
  font-family: var(--font-display);
  font-size: 1.75rem;
  font-weight: 700;
  line-height: 1;
}
.kpi-value.sm {
  font-size: 1.3rem;
}
.kpi-delta {
  font-size: 0.72rem;
  color: var(--text-muted);
  margin-top: 4px;
}
.kpi-delta.up {
  color: var(--green);
}
.kpi-delta.down {
  color: var(--red);
}

/* ═══════════════════════════════════
   DASHBOARD CARDS
═══════════════════════════════════ */
.dash-grid {
  display: grid;
  grid-template-columns: 1fr 360px;
  gap: 20px;
}
.dash-card {
  background: var(--bg-surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 20px;
  box-shadow: var(--shadow-card);
}
.card-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 16px;
}
.card-header h3 {
  font-family: var(--font-display);
  font-size: 0.95rem;
  font-weight: 600;
}

/* ── Alert list ── */
.alert-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
}
.alert-item {
  display: flex;
  align-items: flex-start;
  gap: 12px;
  padding: 12px;
  border-radius: var(--radius-md);
  border: 1px solid transparent;
}
.alert-item i {
  font-size: 18px;
  flex-shrink: 0;
  margin-top: 1px;
}
.alert-item p {
  font-size: 0.85rem;
  font-weight: 500;
}
.alert-item span {
  font-size: 0.75rem;
  color: var(--text-muted);
}
.alert-item.warn {
  background: var(--amber-dim);
  border-color: rgba(245, 158, 11, 0.2);
}
.alert-item.warn i {
  color: var(--amber);
}
.alert-item.info {
  background: var(--blue-dim);
  border-color: rgba(59, 130, 246, 0.2);
}
.alert-item.info i {
  color: var(--blue);
}
.alert-item.success {
  background: var(--green-dim);
  border-color: rgba(34, 197, 94, 0.2);
}
.alert-item.success i {
  color: var(--green);
}
.alert-item.danger {
  background: var(--red-dim);
  border-color: rgba(239, 68, 68, 0.2);
}
.alert-item.danger i {
  color: var(--red);
}

.calculadoradeimc {
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
    background: linear-gradient(
      135deg,
      var(--bg-dark) 0%,
      #1f1f1f 50%,
      var(--bg-dark) 100%
    );
    min-height: 100vh;
    padding: 20px;
    color: var(--text-primary);
  }

  .container {
    max-width: 1000px;
    margin: 0 auto;
  }

  header {
    text-align: center;
    margin-bottom: 30px;
    padding: 30px 20px;
    background: linear-gradient(135deg, var(--bg-card), var(--bg-element));
    border-radius: 12px;
    border: 1px solid var(--border-color);
    box-shadow: var(--shadow-lg);
  }

  header h1 {
    font-size: 2.5rem;
    margin-bottom: 10px;
    color: var(--primary-color);
    text-shadow: 0 0 10px rgba(255, 107, 0, 0.5);
    letter-spacing: 1px;
  }

  .subtitle {
    font-size: 1.1rem;
    color: var(--text-secondary);
  }

  main {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  .card {
    background: var(--bg-card);
    border-radius: 12px;
    padding: 25px;
    box-shadow: var(--shadow-lg);
    border: 1px solid var(--border-color);
  }

  .card h2 {
    color: var(--primary-color);
    margin-bottom: 20px;
    font-size: 1.5rem;
    border-bottom: 3px solid var(--primary-color);
    padding-bottom: 10px;
    display: inline-block;
  }

  /* Formulrio */
  .form-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 15px;
    margin-bottom: 15px;
  }

  .form-group {
    margin-bottom: 15px;
  }

  .form-group label {
    display: block;
    margin-bottom: 8px;
    color: var(--text-primary);
    font-weight: 600;
  }

  .form-group input,
  .form-group select {
    width: 100%;
    padding: 12px 15px;
    border: 2px solid var(--border-color);
    border-radius: 8px;
    font-size: 1rem;
    background: var(--bg-element);
    color: var(--text-primary);
    transition: all 0.3s ease;
  }

  .form-group input::placeholder {
    color: var(--text-muted);
  }

  .form-group input:focus,
  .form-group select:focus {
    outline: none;
    border-color: var(--primary-color);
    box-shadow: var(--glow);
    background: #333333;
  }

  .form-group select {
    cursor: pointer;
  }

  .form-group select option {
    background: var(--bg-element);
    color: var(--text-primary);
  }

  .btn-primary {
    background: linear-gradient(
      135deg,
      var(--primary-color),
      var(--primary-dark)
    );
    color: white;
    border: none;
    padding: 14px 30px;
    border-radius: 8px;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    width: 100%;
    text-transform: uppercase;
    letter-spacing: 1px;
    margin-top: 10px;
  }

  .btn-primary:hover {
    background: linear-gradient(
      135deg,
      var(--primary-light),
      var(--primary-color)
    );
    transform: translateY(-2px);
    box-shadow: var(--glow);
  }

  .btn-secondary {
    background: transparent;
    color: var(--text-secondary);
    border: 2px solid var(--border-color);
    padding: 12px 25px;
    border-radius: 8px;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
  }

  .btn-secondary:hover {
    border-color: var(--primary-color);
    color: var(--primary-color);
    background: var(--bg-element);
  }

  /* Resultados Grid */
  .results-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 15px;
    margin-bottom: 25px;
  }

  .result-item {
    background: var(--bg-element);
    border-radius: 10px;
    padding: 20px;
    display: flex;
    align-items: center;
    gap: 15px;
    border: 1px solid var(--border-color);
    transition: all 0.3s ease;
  }

  .result-item:hover {
    border-color: var(--primary-color);
    transform: translateY(-3px);
    box-shadow: var(--shadow);
  }

  .result-item.highlight {
    background: linear-gradient(135deg, var(--bg-highlight), var(--bg-element));
    border-left: 4px solid var(--primary-color);
  }

  .result-icon {
    font-size: 2.5rem;
    width: 60px;
    height: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: var(--bg-card);
    border-radius: 50%;
    border: 2px solid var(--border-color);
  }

  .result-content {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 5px;
  }

  .result-label {
    color: var(--text-secondary);
    font-size: 0.9rem;
    text-transform: uppercase;
    letter-spacing: 0.5px;
  }

  .result-value {
    color: var(--text-primary);
    font-size: 1.8rem;
    font-weight: 700;
    line-height: 1;
  }

  .result-item.highlight .result-value {
    color: var(--primary-color);
  }

  .result-percent {
    color: var(--primary-light);
    font-size: 1.1rem;
    font-weight: 600;
  }

  .result-classification {
    color: var(--info-color);
    font-size: 0.85rem;
    font-weight: 600;
    text-transform: uppercase;
  }

  .result-detail {
    color: var(--text-muted);
    font-size: 0.8rem;
  }

  .action-buttons {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 15px;
  }

  /* Histrico */
  .history-list {
    display: flex;
    flex-direction: column;
    gap: 12px;
    max-height: 400px;
    overflow-y: auto;
  }

  .history-item {
    background: var(--bg-element);
    border-radius: 8px;
    padding: 15px 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    border-left: 3px solid var(--info-color);
    transition: all 0.3s ease;
    cursor: pointer;
  }

  .history-item:hover {
    border-left-color: var(--primary-color);
    transform: translateX(5px);
    background: var(--bg-highlight);
  }

  .history-info {
    flex: 1;
  }

  .history-info strong {
    color: var(--text-primary);
    font-size: 1.1rem;
    display: block;
    margin-bottom: 5px;
  }

  .history-details {
    color: var(--text-secondary);
    font-size: 0.9rem;
    display: flex;
    gap: 15px;
  }

  .history-date {
    color: var(--text-muted);
    font-size: 0.85rem;
  }

  .history-actions {
    display: flex;
    gap: 10px;
  }

  .btn-icon {
    background: var(--bg-card);
    border: 1px solid var(--border-color);
    color: var(--text-secondary);
    width: 35px;
    height: 35px;
    border-radius: 6px;
    cursor: pointer;
    transition: all 0.3s ease;
    font-size: 1rem;
  }

  .btn-icon:hover {
    border-color: var(--danger-color);
    color: var(--danger-color);
    background: var(--bg-element);
  }

  .empty-state {
    text-align: center;
    padding: 40px 20px;
    color: var(--text-secondary);
  }

  .empty-state svg {
    width: 80px;
    height: 80px;
    margin-bottom: 15px;
    opacity: 0.3;
    stroke: var(--text-muted);
  }

  /* Log */
  .log-list {
    max-height: 300px;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .log-list::-webkit-scrollbar {
    width: 8px;
  }

  .log-list::-webkit-scrollbar-track {
    background: var(--bg-dark);
    border-radius: 4px;
  }

  .log-list::-webkit-scrollbar-thumb {
    background: var(--primary-color);
    border-radius: 4px;
  }

  .log-item {
    padding: 10px 15px;
    background: var(--bg-element);
    border-radius: 6px;
    font-family: "Courier New", monospace;
    font-size: 0.9rem;
    border-left: 3px solid var(--primary-color);
    color: var(--text-secondary);
  }

  .log-item.info {
    border-left-color: var(--primary-color);
  }

  .log-item.success {
    border-left-color: var(--success-color);
    color: var(--success-color);
  }

  .log-item.error {
    border-left-color: var(--danger-color);
    color: var(--danger-color);
  }

  .log-timestamp {
    color: var(--text-muted);
    font-size: 0.8rem;
    margin-right: 10px;
  }

  /* Footer */
  footer {
    text-align: center;
    color: var(--text-secondary);
    margin-top: 30px;
    padding: 20px;
    background: var(--bg-card);
    border-radius: 12px;
    border: 1px solid var(--border-color);
  }

  /* Scrollbar personalizada */
  ::-webkit-scrollbar {
    width: 10px;
  }

  ::-webkit-scrollbar-track {
    background: var(--bg-dark);
  }

  ::-webkit-scrollbar-thumb {
    background: var(--primary-color);
    border-radius: 5px;
  }

  ::-webkit-scrollbar-thumb:hover {
    background: var(--primary-light);
  }

  /* Responsivo */
  @media (max-width: 768px) {
    .form-row {
      grid-template-columns: 1fr;
    }

    .results-grid {
      grid-template-columns: 1fr;
    }

    .action-buttons {
      grid-template-columns: 1fr;
    }

    header h1 {
      font-size: 1.8rem;
    }

    .history-item {
      flex-direction: column;
      gap: 15px;
      text-align: center;
    }

    .history-details {
      justify-content: center;
    }
  }

  /* Efeitos de hover extras */
  .card:hover {
    border-color: var(--border-light);
  }

  .btn-primary:active {
    transform: translateY(0);
  }

  .result-item:active {
    transform: scale(0.98);
  }

  /* Animaes */
  @keyframes fadeIn {
    from {
      opacity: 0;
      transform: translateY(20px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  .card {
    animation: fadeIn 0.5s ease-out;
  }

  .result-item {
    animation: fadeIn 0.3s ease-out;
  }

  .result-item:nth-child(1) {
    animation-delay: 0.05s;
  }
  .result-item:nth-child(2) {
    animation-delay: 0.1s;
  }
  .result-item:nth-child(3) {
    animation-delay: 0.15s;
  }
  .result-item:nth-child(4) {
    animation-delay: 0.3s;
  }
}

/* ═══════════════════════════════════
   TABLES
═══════════════════════════════════ */
.table-card {
  background: var(--bg-surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  overflow: hidden;
  box-shadow: var(--shadow-card);
}
.data-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.875rem;
}
.data-table thead tr {
  background: var(--bg-elevated);
}
.data-table th {
  padding: 12px 16px;
  text-align: left;
  font-size: 0.72rem;
  font-weight: 600;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 0.05em;
  white-space: nowrap;
}
.data-table td {
  padding: 12px 16px;
  border-bottom: 1px solid var(--border);
  color: var(--text-primary);
}
.data-table tbody tr:hover {
  background: var(--bg-hover);
}
.data-table tbody tr:last-child td {
  border-bottom: none;
}

/* ── Status badges ── */
.badge-status {
  display: inline-flex;
  align-items: center;
  gap: 5px;
  padding: 3px 10px;
  border-radius: 20px;
  font-size: 0.72rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.04em;
}
.badge-status::before {
  content: "";
  width: 5px;
  height: 5px;
  border-radius: 50%;
}
.badge-status.ativo {
  background: var(--green-dim);
  color: var(--green);
}
.badge-status.ativo::before {
  background: var(--green);
}
.badge-status.pendente {
  background: var(--amber-dim);
  color: var(--amber);
}
.badge-status.pendente::before {
  background: var(--amber);
}
.badge-status.pago {
  background: var(--green-dim);
  color: var(--green);
}
.badge-status.pago::before {
  background: var(--green);
}
.badge-status.atrasado {
  background: var(--red-dim);
  color: var(--red);
}
.badge-status.atrasado::before {
  background: var(--red);
}
.badge-status.inativo {
  background: var(--bg-elevated);
  color: var(--text-muted);
}
.badge-status.inativo::before {
  background: var(--text-muted);
}

.badge-plano {
  display: inline-block;
  padding: 2px 8px;
  border-radius: var(--radius-sm);
  font-size: 0.72rem;
  font-weight: 600;
}
.badge-plano.basico {
  background: var(--bg-elevated);
  color: var(--text-secondary);
}
.badge-plano.premium {
  background: rgba(59, 130, 246, 0.15);
  color: var(--blue);
}
.badge-plano.black {
  background: rgba(255, 107, 26, 0.15);
  color: var(--accent);
}

/* ── Pagination ── */
.table-pagination {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px 16px;
  border-top: 1px solid var(--border);
  font-size: 0.8rem;
  color: var(--text-muted);
}
.pag-buttons {
  display: flex;
  align-items: center;
  gap: 8px;
}
#pag-info {
  font-size: 0.8rem;
  color: var(--text-secondary);
}

/* ── Filters bar ── */
.filters-bar {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 16px;
  flex-wrap: wrap;
}
.filters-bar select,
.filters-bar .input-icon {
  flex-shrink: 0;
}
.filters-bar select {
  padding: 8px 12px;
  background: var(--bg-surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  font-size: 0.85rem;
  outline: none;
  cursor: pointer;
  transition: border-color var(--trans);
}
.filters-bar select:focus {
  border-color: var(--accent);
}

/* ── Action buttons in rows ── */
.row-actions {
  display: flex;
  gap: 6px;
}

.brand-icon {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  width: 34px;
  height: 34px;
  border-radius: 10px;
  background: var(--accent-dim);
  color: var(--accent);
  font-size: 1.2rem;
}

.btn-primary,
.btn-sm,
.btn-icon,
.tab-btn,
button {
  transition: all var(--trans);
}

.btn-primary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  border: none;
  border-radius: var(--radius-md);
  background: var(--accent);
  color: #fff;
  padding: 10px 14px;
  font-weight: 600;
  box-shadow: var(--shadow-card);
}

.btn-primary:hover {
  background: var(--accent-hover);
}

.btn-sm {
  background: var(--bg-elevated);
  border: 1px solid var(--border);
  color: var(--text-primary);
  border-radius: var(--radius-sm);
  padding: 6px 10px;
  font-size: 0.75rem;
}

.btn-icon {
  width: 30px;
  height: 30px;
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  background: var(--bg-elevated);
  color: var(--text-secondary);
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.btn-icon:hover {
  border-color: var(--border-hover);
  color: var(--text-primary);
}

.input-icon {
  display: flex;
  align-items: center;
  gap: 8px;
  background: var(--bg-elevated);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  padding: 0 12px;
  min-height: 38px;
}

.input-icon input {
  background: transparent;
  border: none;
  outline: none;
  width: 100%;
  padding: 8px 0;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-bottom: 16px;
}

.form-group label {
  color: var(--text-secondary);
  font-size: 0.8rem;
}

.form-group input,
.form-group textarea,
.form-group select {
  width: 100%;
  background: var(--bg-elevated);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  padding: 10px 12px;
  outline: none;
}

.form-group input:focus,
.form-group textarea:focus,
.form-group select:focus {
  border-color: var(--accent);
}

.config-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 20px;
}

.config-card {
  background: var(--bg-surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 18px;
  box-shadow: var(--shadow-card);
}

.config-card h3 {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-bottom: 16px;
  font-family: var(--font-display);
}

.toggle-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-direction: row;
}

.toggle {
  position: relative;
  display: inline-flex;
  align-items: center;
}

.toggle input {
  display: none;
}

.toggle-track {
  position: relative;
  width: 42px;
  height: 24px;
  background: var(--bg-elevated);
  border: 1px solid var(--border);
  border-radius: 30px;
  display: block;
}

.toggle-track::after {
  content: "";
  position: absolute;
  width: 16px;
  height: 16px;
  background: #fff;
  border-radius: 50%;
  left: 3px;
  top: 3px;
  transition: all var(--trans);
}

.toggle input:checked + .toggle-track {
  background: var(--green-dim);
  border-color: rgba(34, 197, 94, 0.4);
}

.toggle input:checked + .toggle-track::after {
  left: 21px;
  background: var(--green);
}

.treino-tabs {
  display: flex;
  gap: 8px;
  margin-bottom: 16px;
  flex-wrap: wrap;
}

.tab-btn {
  background: var(--bg-surface);
  color: var(--text-secondary);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  padding: 8px 12px;
  font-weight: 600;
}

.tab-btn.active {
  background: var(--accent-dim);
  color: var(--accent);
  border-color: rgba(255, 107, 26, 0.25);
}

.treinos-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 18px;
}

.treino-card {
  background: var(--bg-surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 16px;
  box-shadow: var(--shadow-card);
}

.treino-card-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 10px;
  margin-bottom: 12px;
}

.treino-card-header h3 {
  font-size: 1rem;
  font-family: var(--font-display);
}

.treino-type-badge {
  display: inline-block;
  padding: 4px 8px;
  border-radius: 999px;
  font-size: 0.7rem;
  background: var(--bg-elevated);
  color: var(--text-secondary);
}

.treino-card-body table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 12px;
  font-size: 0.75rem;
}

.treino-card-body th,
.treino-card-body td {
  padding: 6px 4px;
  text-align: left;
  border-bottom: 1px solid var(--border);
}

.imc-form {
  display: flex;
  flex-direction: column;
  gap: 12px;
  max-width: 420px;
  margin-bottom: 20px;
}

.imc-result {
  min-height: 30px;
  color: var(--text-primary);
  font-weight: 600;
}

.empty-state {
  background: var(--bg-surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 24px;
  text-align: center;
  color: var(--text-secondary);
}

/* ─────────────────────────────────────────
   MODAL
───────────────────────────────────────── */
.modal {
  display: none;
  align-items: center;
  justify-content: center;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.6);
  z-index: 1000;
  animation: fadeIn 0.2s ease;
}

.modal.open {
  display: flex;
}

.modal-content {
  background: var(--bg-surface);
  border-radius: var(--radius-lg);
  padding: 24px;
  max-width: 500px;
  width: 90%;
  max-height: 90vh;
  overflow-y: auto;
  box-shadow: var(--shadow-modal);
  position: relative;
  animation: slideUp 0.3s ease;
}

.modal-close {
  position: absolute;
  top: 12px;
  right: 12px;
  background: none;
  border: none;
  color: var(--text-secondary);
  font-size: 28px;
  cursor: pointer;
  transition: color var(--trans);
}

.modal-close:hover {
  color: var(--text-primary);
}

.modal h2 {
  margin-bottom: 16px;
  color: var(--text-primary);
  font-family: var(--font-display);
}

/* ─────────────────────────────────────────
   FORM ELEMENTS
───────────────────────────────────────── */
.form-group {
  margin-bottom: 16px;
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.form-group label {
  color: var(--text-primary);
  font-size: 0.9rem;
  font-weight: 500;
}

.form-group input,
.form-group select,
.form-group textarea {
  background: var(--bg-void);
  border: 1px solid var(--border);
  padding: 10px 12px;
  border-radius: var(--radius-md);
  color: var(--text-primary);
  transition: border-color var(--trans);
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  outline: none;
  border-color: var(--accent);
  box-shadow: 0 0 0 3px var(--accent-dim);
}

.form-group small {
  font-size: 0.8rem;
  color: var(--text-muted);
  margin-top: 4px;
}

.form-actions {
  display: flex;
  gap: 12px;
  justify-content: flex-end;
  margin-top: 20px;
}

/* ─────────────────────────────────────────
   ANIMATIONS
───────────────────────────────────────── */
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes slideUp {
  from {
    transform: translateY(20px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}

@keyframes slideIn {
  from {
    transform: translateX(400px);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

@keyframes slideOut {
  from {
    transform: translateX(0);
    opacity: 1;
  }
  to {
    transform: translateX(400px);
    opacity: 0;
  }
}

/* ─────────────────────────────────────────
   PROGRESSO
───────────────────────────────────────── */
.progress-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 20px;
  margin-bottom: 24px;
}

.progress-card {
  background: var(--bg-surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 20px;
  box-shadow: var(--shadow-card);
}

.progress-card h3 {
  margin-bottom: 16px;
  color: var(--text-primary);
  font-family: var(--font-display);
  font-size: 1.1rem;
}

/* Gráfico de Barras */
.chart-container {
  width: 100%;
  height: 200px;
  padding: 12px 0;
}

.bar-chart {
  display: flex;
  align-items: flex-end;
  justify-content: space-around;
  height: 100%;
  gap: 12px;
}

.bar-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
}

.bar-item .bar {
  width: 100%;
  background: linear-gradient(to top, var(--accent), var(--accent-hover));
  border-radius: var(--radius-md) var(--radius-md) 0 0;
  min-height: 4px;
  transition: all var(--trans);
  cursor: pointer;
}

.bar-item .bar:hover {
  filter: brightness(1.1);
  box-shadow: 0 0 8px var(--accent-glow);
}

.bar-label {
  font-size: 0.8rem;
  color: var(--text-secondary);
  font-weight: 500;
}

.bar-value {
  font-size: 0.9rem;
  color: var(--text-primary);
  font-weight: 600;
}

/* Progress Bar para Metas */
.meta-item {
  margin-bottom: 16px;
}

.meta-item label {
  display: block;
  font-size: 0.9rem;
  color: var(--text-primary);
  margin-bottom: 6px;
  font-weight: 500;
}

.progress-bar {
  width: 100%;
  height: 24px;
  background: var(--bg-void);
  border-radius: var(--radius-md);
  overflow: hidden;
  border: 1px solid var(--border);
  position: relative;
}

.progress-fill {
  height: 100%;
  background: linear-gradient(90deg, var(--green), var(--green-dim));
  border-radius: var(--radius-md);
  transition: width 0.4s ease;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  padding-right: 6px;
}

.progress-text {
  font-size: 0.75rem;
  color: var(--text-secondary);
  margin-top: 4px;
  display: block;
  text-align: right;
}

/* Conquistas */
.achievements-section {
  background: var(--bg-surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 20px;
  margin-top: 20px;
}

.achievements-section h3 {
  margin-bottom: 16px;
  color: var(--text-primary);
  font-family: var(--font-display);
}

.achievements-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 12px;
}

.achievement-badge {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 8px;
  padding: 16px 12px;
  background: var(--bg-elevated);
  border: 2px solid var(--accent);
  border-radius: var(--radius-lg);
  cursor: pointer;
  transition: all var(--trans);
  text-align: center;
}

.achievement-badge:hover {
  transform: translateY(-4px);
  box-shadow: 0 4px 16px var(--accent-glow);
  background: var(--accent-dim);
}

.achievement-badge i {
  font-size: 2rem;
  color: var(--accent);
}

.achievement-badge span {
  font-size: 0.85rem;
  color: var(--text-primary);
  font-weight: 600;
}

/* ─────────────────────────────────────────
   MEUS TREINOS
───────────────────────────────────────── */

.treino-tabs {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  margin-bottom: 24px;
  border-bottom: 1px solid var(--border);
  padding-bottom: 12px;
}

.tab-btn {
  background: transparent;
  border: none;
  padding: 10px 16px;
  color: var(--text-secondary);
  font-size: 0.95rem;
  font-weight: 500;
  cursor: pointer;
  transition: all var(--trans);
  border-bottom: 2px solid transparent;
  display: flex;
  align-items: center;
  gap: 6px;
}

.tab-btn:hover {
  color: var(--text-primary);
}

.tab-btn.active {
  color: var(--accent);
  border-bottom-color: var(--accent);
}

.tab-btn i {
  font-size: 1.1rem;
}

.treinos-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(380px, 1fr));
  gap: 20px;
  margin-bottom: 24px;
}

.treino-card {
  background: var(--bg-surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  overflow: hidden;
  box-shadow: var(--shadow-card);
  display: flex;
  flex-direction: column;
  transition: all var(--trans);
}

.treino-card:hover {
  border-color: var(--accent);
  transform: translateY(-4px);
  box-shadow: 0 8px 24px var(--accent-glow);
}

.treino-card-header {
  padding: 16px;
  background: var(--bg-elevated);
  border-bottom: 1px solid var(--border);
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 12px;
}

.treino-card-header h3 {
  margin: 0;
  font-size: 1.1rem;
  color: var(--text-primary);
  font-family: var(--font-display);
}

.treino-type-badge {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  padding: 6px 12px;
  border-radius: 999px;
  font-size: 0.8rem;
  font-weight: 600;
  background: var(--accent-dim);
  color: var(--accent);
  width: fit-content;
}

.treino-type-badge.musculacao {
  background: rgba(255, 107, 26, 0.15);
  color: #ff6b1a;
}

.treino-type-badge.crossfit {
  background: rgba(59, 130, 246, 0.15);
  color: #3b82f6;
}

.treino-type-badge.fisioterapia {
  background: rgba(34, 197, 94, 0.15);
  color: #22c55e;
}

.treino-actions {
  display: flex;
  gap: 4px;
}

.btn-icon-sm {
  background: none;
  border: none;
  color: var(--text-secondary);
  cursor: pointer;
  padding: 6px;
  font-size: 1.2rem;
  transition: all var(--trans);
  border-radius: var(--radius-md);
}

.btn-icon-sm:hover {
  background: var(--bg-hover);
  color: var(--accent);
}

.btn-icon-sm.danger:hover {
  background: rgba(239, 68, 68, 0.15);
  color: var(--red);
}

.treino-card-body {
  padding: 16px;
  flex: 1;
  overflow: auto;
}

.treino-obs {
  font-size: 0.85rem;
  color: var(--text-secondary);
  margin-bottom: 12px;
  padding: 8px 10px;
  background: var(--bg-void);
  border-left: 3px solid var(--accent);
  border-radius: var(--radius-sm);
  display: flex;
  gap: 6px;
  align-items: flex-start;
}

.treino-obs i {
  flex-shrink: 0;
  margin-top: 2px;
}

.treino-exercicios h4 {
  font-size: 0.9rem;
  color: var(--text-primary);
  margin: 0 0 10px 0;
  font-weight: 600;
}

.treino-exercicios table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.85rem;
}

.treino-exercicios th,
.treino-exercicios td {
  padding: 8px 4px;
  text-align: left;
  border-bottom: 1px solid var(--border);
  color: var(--text-secondary);
}

.treino-exercicios th {
  font-weight: 600;
  color: var(--text-primary);
  background: var(--bg-void);
}

.treino-exercicios td {
  color: var(--text-secondary);
}

.treino-card-footer {
  padding: 12px 16px;
  background: var(--bg-elevated);
  border-top: 1px solid var(--border);
  display: flex;
  gap: 8px;
}

.btn-primary-sm {
  flex: 1;
  background: linear-gradient(135deg, var(--accent), var(--accent-hover));
  color: white;
  border: none;
  padding: 10px 16px;
  border-radius: var(--radius-md);
  font-size: 0.9rem;
  font-weight: 600;
  cursor: pointer;
  transition: all var(--trans);
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 6px;
}

.btn-primary-sm:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px var(--accent-glow);
}

.btn-primary-sm:active {
  transform: translateY(0);
}

/* Badge Compartilhado */
.badge-compartilhado {
  display: inline-flex;
  align-items: center;
  gap: 4px;
  padding: 6px 12px;
  border-radius: 999px;
  font-size: 0.75rem;
  font-weight: 600;
  background: var(--green-dim);
  color: var(--green);
  margin-left: 8px;
}

/* Modal Execução Treino */
.modal-execucao-content {
  max-width: 600px;
  max-height: 90vh;
  display: flex;
  flex-direction: column;
}

.exec-header {
  padding: 20px;
  background: var(--bg-elevated);
  border-bottom: 1px solid var(--border);
  flex-shrink: 0;
}

.exec-header h2 {
  margin: 0 0 12px 0;
  font-size: 1.4rem;
  color: var(--text-primary);
}

.exec-progress {
  width: 100%;
  height: 8px;
  background: var(--bg-active);
  border-radius: 999px;
  overflow: hidden;
  margin-bottom: 8px;
}

.exec-progress-bar {
  height: 100%;
  background: linear-gradient(90deg, var(--accent), var(--accent-hover));
  transition: width 0.3s ease;
  width: 0%;
}

.exec-body {
  flex: 1;
  overflow-y: auto;
  padding: 20px;
}

.exec-exercicio-info {
  text-align: center;
}

.exec-exercicio-info h2 {
  font-size: 2rem;
  color: var(--accent);
  margin-bottom: 20px;
  font-family: var(--font-display);
}

.exec-detalhes {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
  margin-bottom: 20px;
}

.detalhe {
  background: var(--bg-surface);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 16px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 6px;
}

.detalhe .label {
  font-size: 0.8rem;
  color: var(--text-secondary);
  text-transform: uppercase;
  font-weight: 600;
}

.detalhe .valor {
  font-size: 1.5rem;
  color: var(--text-primary);
  font-family: var(--font-display);
  font-weight: 700;
}

.exec-actions {
  display: flex;
  gap: 12px;
  padding: 16px 20px;
  background: var(--bg-elevated);
  border-top: 1px solid var(--border);
  flex-shrink: 0;
  justify-content: space-between;
}

.exec-actions .btn-sm,
.exec-actions .btn-primary-sm {
  flex: 1;
  padding: 12px;
  font-weight: 600;
}

.exec-actions .btn-sm.danger {
  background: var(--red-dim);
  color: var(--red);
  border: 1px solid var(--red);
}

.exec-actions .btn-sm.danger:hover {
  background: rgba(239, 68, 68, 0.3);
}

/* Responsividade */
@media (max-width: 768px) {
  .treinos-grid {
    grid-template-columns: 1fr;
  }

  .treino-tabs {
    flex-wrap: nowrap;
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
  }

  .treino-card-header {
    flex-wrap: wrap;
  }
}
