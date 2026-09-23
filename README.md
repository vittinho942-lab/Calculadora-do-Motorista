<!DOCTYPE html>
<html lang="pt">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Calculadora do Motorista</title>
    <style>
        :root {
            --bg-color: #121212;
            --card-bg: #1e1e1e;
            --text-color: #e0e0e0;
            --primary-color: #00e676;
            --border-color: #333;
            --input-bg: #2a2a2a;
            --danger-color: #ff5252;
            --edit-color: #ffb74d;
            --reserve-color: #29b6f6;
            --uber-purple: #b388ff;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            margin: 0;
            padding: 8px;
        }
        .container {
            max-width: 500px;
            margin: 0 auto;
            background: var(--card-bg);
            padding: 12px;
            border-radius: 12px;
            box-shadow: 0 4px 15px rgba(0,0,0,0.5);
            position: relative;
        }
        .header-top {
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: relative;
            margin-bottom: 10px;
        }
        h1 {
            text-align: center;
            color: var(--primary-color);
            font-size: 1.5rem;
            margin: 0;
            flex: 1;
        }
        .menu-dots-btn {
            background: none;
            border: none;
            color: var(--text-color);
            font-size: 1.5rem;
            cursor: pointer;
            padding: 0 8px;
            font-weight: bold;
        }
        .menu-dropdown {
            display: none;
            position: absolute;
            right: 0;
            top: 40px;
            background: #222;
            border: 1px solid var(--border-color);
            border-radius: 8px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.6);
            z-index: 100;
            width: 200px;
            padding: 6px;
        }
        .menu-dropdown.show {
            display: block;
        }
        .menu-dropdown button {
            background: none;
            border: none;
            color: var(--text-color);
            width: 100%;
            text-align: left;
            padding: 8px;
            font-size: 0.9rem;
            cursor: pointer;
            border-radius: 4px;
        }
        .menu-dropdown button:hover {
            background: var(--input-bg);
            color: var(--primary-color);
        }

        .tabs {
            display: flex;
            justify-content: space-around;
            margin-bottom: 12px;
            background: var(--input-bg);
            padding: 4px;
            border-radius: 8px;
            overflow-x: auto;
        }
        .tab-btn {
            background: none;
            border: none;
            color: var(--text-color);
            padding: 8px 10px;
            cursor: pointer;
            border-radius: 6px;
            font-weight: bold;
            font-size: 0.85rem;
            white-space: nowrap;
        }
        .tab-btn.active {
            background: var(--primary-color);
            color: #121212;
        }
        .form-group {
            margin-bottom: 10px;
        }
        label {
            display: block;
            font-size: 0.85rem;
            margin-bottom: 3px;
            color: #ccc;
        }
        input, select {
            width: 100%;
            padding: 10px;
            background: var(--input-bg);
            border: 1px solid var(--border-color);
            color: var(--text-color);
            border-radius: 6px;
            font-size: 1.05rem;
            box-sizing: border-box;
        }
        .cronometro-box {
            display: flex;
            gap: 8px;
            align-items: center;
        }
        .cronometro-box input {
            flex: 1;
            background: #181818;
            font-weight: bold;
            color: var(--primary-color);
        }
        .btn-chrono {
            padding: 10px 15px;
            border: none;
            border-radius: 6px;
            font-weight: bold;
            cursor: pointer;
            font-size: 0.9rem;
        }
        .btn-start { background: #00e676; color: #121212; }
        .btn-stop { background: var(--danger-color); color: #fff; }
        
        .results {
            margin-top: 15px;
            background: #181818;
            padding: 12px;
            border-radius: 8px;
            border: 1px solid var(--border-color);
        }
        .results h3 {
            margin: 0 0 10px 0;
            color: var(--primary-color);
            font-size: 1.2rem;
            text-align: center;
        }
        .result-item {
            display: flex;
            justify-content: space-between;
            margin-bottom: 8px;
            font-size: 1rem;
        }
        .result-item span:last-child {
            font-weight: bold;
            color: var(--primary-color);
        }
        .sobra-livre-box {
            background: rgba(0, 230, 118, 0.12);
            border: 2px dashed var(--primary-color);
            padding: 12px;
            border-radius: 8px;
            margin-top: 10px;
            text-align: center;
        }
        .sobra-livre-val {
            font-size: 1.8rem;
            font-weight: bold;
            color: var(--primary-color);
        }
        .btn-action {
            width: 100%;
            padding: 12px;
            background: var(--primary-color);
            color: #121212;
            border: none;
            border-radius: 6px;
            font-weight: bold;
            font-size: 1.1rem;
            cursor: pointer;
            margin-top: 10px;
        }
        .section-title {
            color: var(--primary-color);
            font-size: 1.2rem;
            margin-top: 10px;
            margin-bottom: 8px;
            text-align: center;
            border-bottom: 1px solid var(--border-color);
            padding-bottom: 5px;
        }
        .card-box {
            background: #181818;
            padding: 12px;
            margin-bottom: 12px;
            border-radius: 12px;
            border: 1px solid var(--border-color);
        }
        
        .chart-container-semana {
            display: flex;
            justify-content: space-between;
            align-items: flex-end;
            height: 150px;
            padding: 12px 6px;
            margin: 10px 0;
            background: #141414;
            border-radius: 8px;
            overflow-x: auto;
            gap: 4px;
            border: 1px solid var(--border-color);
        }
        .chart-col {
            display: flex;
            flex-direction: column;
            align-items: center;
            min-width: 20px;
            flex: 1;
            cursor: pointer;
            padding: 2px;
            border-radius: 4px;
            transition: background 0.2s;
        }
        .chart-col:hover {
            background: rgba(179, 136, 255, 0.15);
        }
        .chart-bar-wrapper {
            height: 90px;
            display: flex;
            align-items: flex-end;
            margin-bottom: 4px;
        }
        .chart-bar {
            width: 10px;
            background: #3a3a3a;
            border-radius: 4px 4px 0 0;
            transition: height 0.3s ease;
        }
        .chart-bar.active {
            background: var(--uber-purple);
            box-shadow: 0 0 8px rgba(179, 136, 255, 0.6);
        }
        .chart-val {
            font-size: 0.55rem;
            color: #aaa;
            margin-bottom: 3px;
            height: 10px;
            white-space: nowrap;
        }
        .chart-col:hover .chart-val {
            color: #fff;
        }
        .chart-day {
            font-size: 0.65rem;
            color: #ccc;
            font-weight: bold;
        }

        .mensal-hero {
            background: linear-gradient(135deg, #181818, #222222);
            border: 1px solid var(--border-color);
            border-radius: 12px;
            padding: 14px 10px;
            text-align: center;
            margin-bottom: 12px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.4);
        }
        .mes-seletor-container {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            background: #282828;
            border: 1px solid var(--primary-color);
            border-radius: 20px;
            padding: 4px 12px;
            margin-bottom: 10px;
        }
        .mes-seletor-container input[type="month"] {
            background: transparent;
            border: none;
            color: var(--primary-color);
            font-size: 0.95rem;
            font-weight: bold;
            text-align: center;
            cursor: pointer;
            outline: none;
            padding: 4px;
        }
        .mensal-hero-label {
            font-size: 0.75rem;
            color: #aaa;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-top: 4px;
        }
        .mensal-hero-value {
            font-size: 2.1rem;
            font-weight: bold;
            color: #fff;
            margin: 4px 0 10px 0;
        }
        
        .calendar-grid {
            display: grid;
            grid-template-columns: repeat(7, 1fr);
            gap: 4px;
            margin-top: 8px;
            background: #141414;
            padding: 8px;
            border-radius: 8px;
            border: 1px solid var(--border-color);
        }
        .calendar-header-day {
            font-size: 0.7rem;
            color: var(--primary-color);
            font-weight: bold;
            text-align: center;
            padding-bottom: 4px;
        }
        .calendar-day-cell {
            background: #222;
            border-radius: 6px;
            min-height: 48px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            padding: 4px;
            cursor: pointer;
            border: 1px solid #2c2c2c;
            transition: all 0.2s;
        }
        .calendar-day-cell:hover {
            border-color: var(--uber-purple);
        }
        .calendar-day-cell.empty {
            background: transparent;
            border: none;
            cursor: default;
        }
        .calendar-day-cell.worked {
            background: rgba(179, 136, 255, 0.15);
            border-color: var(--uber-purple);
        }
        .cal-day-num {
            font-size: 0.65rem;
            color: #aaa;
            font-weight: bold;
            text-align: left;
        }
        .calendar-day-cell.worked .cal-day-num {
            color: #fff;
        }
        .cal-day-val {
            font-size: 0.6rem;
            font-weight: bold;
            color: var(--uber-purple);
            text-align: center;
            margin-bottom: 2px;
        }

        .mensal-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-bottom: 12px;
        }
        .mensal-mini-card {
            background: #181818;
            padding: 12px;
            border-radius: 10px;
            border: 1px solid var(--border-color);
            border-left: 4px solid var(--primary-color);
            text-align: left;
        }
        .mensal-mini-card.km { border-left-color: #00bcd4; }
        .mensal-mini-card.vkm { border-left-color: #ab47bc; }
        .mensal-mini-card.vhr { border-left-color: #ffeb3b; }
        .mensal-mini-card.ipva { border-left-color: #2196F3; }
        .mensal-mini-card.manut { border-left-color: #FF9800; }
        .mensal-mini-card.caix { border-left-color: #E91E63; }

        .mensal-mini-card span {
            font-size: 0.75rem;
            color: #bbb;
            text-transform: uppercase;
            display: block;
            margin-bottom: 4px;
        }
        .mensal-mini-card h4 {
            margin: 0;
            font-size: 1.15rem;
            color: #fff;
        }
        .mensal-footer-stats {
            background: #181818;
            border: 1px solid var(--border-color);
            border-radius: 10px;
            padding: 12px 15px;
        }
        .btn-sm {
            padding: 6px 10px;
            font-size: 0.85rem;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
        }
        .btn-edit { background: var(--edit-color); color: #121212; }
        .btn-delete { background: var(--danger-color); color: #fff; }
        .historico-item {
            background: #181818;
            padding: 12px;
            border-radius: 8px;
            margin-bottom: 8px;
            border: 1px solid var(--border-color);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .dia-semana-edit-card {
            background: #222;
            border: 1px solid var(--edit-color);
            border-radius: 8px;
            padding: 12px;
            margin-bottom: 15px;
        }
    </style>
</head>
<body>

<div class="container">
    <div class="header-top">
        <h1>Calculadora do Motorista</h1>
        <button class="menu-dots-btn" onclick="toggleMenuDropdown(event)">⋮</button>
        <div id="menuDropdown" class="menu-dropdown">
            <button onclick="mudarTab('manutencaoCarro')">🔧 Manutenção do Carro</button>
        </div>
    </div>
    
    <div class="tabs">
        <button class="tab-btn active" onclick="mudarTab('diario')">Diário</button>
        <button class="tab-btn" onclick="mudarTab('semana')">Semanal</button>
        <button class="tab-btn" onclick="mudarTab('mensal')">Mensal</button>
        <button class="tab-btn" onclick="mudarTab('config')">Custos</button>
        <button class="tab-btn" onclick="mudarTab('historico')">Histórico</button>
    </div>

    <!-- ABA DIÁRIA -->
    <div id="tabDiario">
        <div class="form-group">
            <label>Data</label>
            <input type="date" id="dataRegistro">
        </div>

        <div class="form-group">
            <label>Dia da Semana</label>
            <select id="diaSemana">
                <option value="Segunda-feira">Segunda-feira</option>
                <option value="Terça-feira">Terça-feira</option>
                <option value="Quarta-feira">Quarta-feira</option>
                <option value="Quinta-feira">Quinta-feira</option>
                <option value="Sexta-feira">Sexta-feira</option>
                <option value="Sábado">Sábado</option>
                <option value="Domingo">Domingo</option>
            </select>
        </div>

        <div class="form-group">
            <label>Faturamento Bruto (R$)</label>
            <input type="number" id="bruto" placeholder="0.00" oninput="calcular()">
        </div>

        <div style="display: flex; gap: 10px;">
            <div class="form-group" style="flex:1;">
                <label>KM Inicial</label>
                <input type="number" id="kmInicial" placeholder="0" oninput="calcular()">
            </div>
            <div class="form-group" style="flex:1;">
                <label>KM Final</label>
                <input type="number" id="kmFinal" placeholder="0" oninput="calcular()">
            </div>
        </div>

        <div class="form-group">
            <label>Horas Online</label>
            <div class="cronometro-box">
                <input type="text" id="horasOnline" value="0.00" oninput="calcular()">
                <button type="button" id="btnChrono" class="btn-chrono btn-start" onclick="toggleCronometro()">Iniciar</button>
            </div>
        </div>

        <div style="display: flex; gap: 10px;">
            <div class="form-group" style="flex:1;">
                <label>Média do Carro (KM/L)</label>
                <input type="number" id="mediaKmLitro" value="10" oninput="calcular()">
            </div>
            <div class="form-group" style="flex:1;">
                <label>Preço do Litro (R$)</label>
                <input type="number" id="precoLitro" value="4.09" oninput="calcular()">
            </div>
        </div>

        <div style="display: flex; gap: 10px;">
            <div class="form-group" style="flex:1;">
                <label>Litros Abastecidos</label>
                <input type="number" id="litros" placeholder="0" oninput="calcularCombustivelPorLitros()">
            </div>
            <div class="form-group" style="flex:1;">
                <label>Valor Abastecido (R$)</label>
                <input type="number" id="valorAbastecido" placeholder="0.00" oninput="calcular()">
            </div>
        </div>

        <div class="form-group">
            <label>Gastos na Rua (Alimentação, etc.)</label>
            <input type="number" id="gastosRua" placeholder="0.00" oninput="calcular()">
        </div>

        <!-- CUSTOS FIXOS DO DIA -->
        <div style="background: #181818; padding: 10px; border-radius: 8px; border: 1px solid var(--border-color); margin-bottom: 10px;">
            <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 5px;">
                <div style="font-size: 0.9rem; color: var(--edit-color); font-weight: bold;">Custo Fixo Automático do Dia</div>
                <button type="button" class="btn-sm btn-edit" onclick="mudarTab('config')">Alterar Mensal</button>
            </div>
            <div style="display: flex; gap: 8px;">
                <div class="form-group" style="flex:1; margin-bottom:0;">
                    <label style="font-size:0.8rem;">Parcela Proporcional</label>
                    <input type="number" id="parcelaCarro" readonly style="color: var(--edit-color); font-weight:bold;">
                </div>
                <div class="form-group" style="flex:1; margin-bottom:0;">
                    <label style="font-size:0.8rem;">Seguro Proporcional</label>
                    <input type="number" id="seguroCarro" readonly style="color: var(--edit-color); font-weight:bold;">
                </div>
            </div>
        </div>

        <!-- RESERVAS / CAIXINHAS DIÁRIAS -->
        <div style="background: #181818; padding: 10px; border-radius: 8px; border: 1px solid var(--border-color); margin-bottom: 10px;">
            <div style="font-size: 0.9rem; color: var(--reserve-color); font-weight: bold; margin-bottom: 8px; text-align: center;">Reservas Separadas por Ocasião</div>
            <div style="display: flex; gap: 8px;">
                <div class="form-group" style="flex:1; margin-bottom:0;">
                    <label style="font-size:0.8rem;">Reserva IPVA (R$)</label>
                    <input type="number" id="reservaIpva" placeholder="0.00" value="10.00" oninput="calcular()">
                </div>
                <div class="form-group" style="flex:1; margin-bottom:0;">
                    <label style="font-size:0.8rem;">Reserva Manut. (R$)</label>
                    <input type="number" id="reservaManutencao" placeholder="0.00" value="15.00" oninput="calcular()">
                </div>
                <div class="form-group" style="flex:1; margin-bottom:0;">
                    <label style="font-size:0.8rem;">Caixinha (R$)</label>
                    <input type="number" id="reservaCaixinha" placeholder="0.00" value="10.00" oninput="calcular()">
                </div>
            </div>
        </div>

        <div class="results">
            <h3>Resumo do Dia</h3>
            <div class="result-item"><span>KM Rodados:</span> <span id="resKm">0 km</span></div>
            <div class="result-item"><span>Gasto Combustível:</span> <span id="resCombustivel">R$ 0,00</span></div>
            <div class="result-item"><span>Custos Fixos do Dia:</span> <span id="resCustosFixos">R$ 0,00</span></div>
            <div class="result-item"><span>Gastos na Rua:</span> <span id="resGastosRua">R$ 0,00</span></div>
            <div class="result-item"><span>Média por Hora:</span> <span id="resPorHora">R$ 0,00 /h</span></div>
            <div class="result-item"><span>Faturamento por KM:</span> <span id="resPorKm">R$ 0,00 /km</span></div>
            
            <div class="sobra-livre-box">
                <div style="font-size: 0.8rem; color: #ccc; text-transform: uppercase;">Quanto Sobra Livre Hoje</div>
                <div class="sobra-livre-val" id="resLiquido">R$ 0,00</div>
            </div>
        </div>

        <input type="hidden" id="editIndex" value="-1">
        <button class="btn-action" id="btnSalvar" onclick="salvarDia()">Salvar Dia no Histórico</button>
    </div>

    <!-- ABA MANUTENÇÃO DO CARRO -->
    <div id="tabManutencaoCarro" style="display: none;">
        <div class="section-title">Controle de Manutenção do Carro</div>
        <div style="font-size: 0.8rem; color: var(--edit-color); text-align: center; margin-bottom: 10px;">
            Registe o que foi trocado, com quantos KM fez e com quantos KM vai refazer.
        </div>

        <div class="results" style="text-align: left; padding: 12px; margin-bottom: 12px;">
            <div class="form-group">
                <label>O que foi mexido / Serviço</label>
                <input type="text" id="manutServico" placeholder="Ex: Troca de óleo, pastilhas de freio...">
            </div>
            <div style="display: flex; gap: 8px;">
                <div class="form-group" style="flex:1;">
                    <label>KM que Fez</label>
                    <input type="number" id="manutKmFeito" placeholder="Ex: 50000">
                </div>
                <div class="form-group" style="flex:1;">
                    <label>KM para Refazer</label>
                    <input type="number" id="manutKmRefazer" placeholder="Ex: 60000">
                </div>
            </div>
            <div class="form-group">
                <label>Custo (R$) - Opcional</label>
                <input type="number" id="manutCusto" placeholder="0.00">
            </div>
            <button class="btn-action" style="margin-top: 5px;" onclick="salvarManutencaoCarro()">Adicionar Manutenção</button>
        </div>

        <div class="section-title" style="font-size: 1rem; margin-top: 15px;">Histórico de Manutenções</div>
        <div id="listaManutencoesCarro" style="max-height: 350px; overflow-y: auto;"></div>
        
        <button class="btn-action" style="background: var(--input-bg); color: #fff; margin-top: 15px;" onclick="mudarTab('diario')">Voltar ao Diário</button>
    </div>

    <!-- ABA CONFIGURAÇÃO DE CUSTOS FIXOS MENSAIS -->
    <div id="tabConfig" style="display: none;">
        <div class="section-title">Configuração de Custos Fixos Mensais</div>
        <div class="results" style="text-align: left; padding: 15px;">
            <div class="form-group">
                <label>Parcela Mensal do Carro (R$)</label>
                <input type="number" id="cfgParcelaMensal" value="1375" oninput="salvarConfiguracoes()">
            </div>
            <div class="form-group">
                <label>Seguro Mensal (R$)</label>
                <input type="number" id="cfgSeguroMensal" value="0.00" oninput="salvarConfiguracoes()">
            </div>
            <div class="form-group">
                <label>Dias Trabalhados Esperados no Mês</label>
                <input type="number" id="cfgDiasMes" value="26" oninput="salvarConfiguracoes()">
            </div>
            <button class="btn-action" onclick="mudarTab('diario')">Salvar e Voltar ao Diário</button>
        </div>
    </div>

    <!-- ABA SEMANAL -->
    <div id="tabSemana" style="display: none;">
        <div class="section-title">Resumo e Finanças Semanais</div>
        <div style="font-size: 0.8rem; color: var(--edit-color); text-align: center; margin-bottom: 10px;">
            Clique em qualquer barra do dia abaixo para editar as informações!
        </div>
        <div id="listaSemanal"></div>
    </div>

    <!-- ABA MENSAL -->
    <div id="tabMensal" style="display: none;">
        <div class="section-title">Balanço do Mês</div>
        
        <div class="mensal-hero">
            <div class="mes-seletor-container">
                <input type="month" id="filtroMesAno" onchange="renderizarMensal()">
            </div>

            <div class="mensal-hero-label">Ganhos Totais do Mês (Bruto)</div>
            <div id="mesBrutoGrande" class="mensal-hero-value">R$ 0,00</div>
            
            <div style="font-size: 0.7rem; color: var(--edit-color); text-align: center; margin-bottom: 4px; font-weight: bold;">
                Calendário do Mês (Toque em um dia trabalhado para editar):
            </div>
            
            <div class="calendar-grid">
                <div class="calendar-header-day">Seg</div>
                <div class="calendar-header-day">Ter</div>
                <div class="calendar-header-day">Qua</div>
                <div class="calendar-header-day">Qui</div>
                <div class="calendar-header-day">Sex</div>
                <div class="calendar-header-day">Sáb</div>
                <div class="calendar-header-day">Dom</div>
            </div>
            <div class="calendar-grid" id="calendarDaysContainer" style="margin-top: 2px;"></div>
        </div>

        <div id="painelEdicaoMensal"></div>

        <div class="sobra-livre-box" style="margin-top: 0; margin-bottom: 12px;">
            <div style="font-size: 0.8rem; color: #ccc; text-transform: uppercase;">Quanto Sobrou no Mês (Líquido)</div>
            <div class="sobra-livre-val" id="mesLiquido">R$ 0,00</div>
        </div>

        <div class="mensal-grid">
            <div class="mensal-mini-card km">
                <span>Total KM Rodados</span>
                <h4 id="mesKmTotal">0 km</h4>
            </div>
            <div class="mensal-mini-card vkm">
                <span>Fat. por KM</span>
                <h4 id="mesValorKm">R$ 0,00</h4>
            </div>
            <div class="mensal-mini-card vhr">
                <span>Fat. por Hora</span>
                <h4 id="mesValorHr">R$ 0,00</h4>
            </div>
            <div class="mensal-mini-card ipva">
                <span>Guardado IPVA</span>
                <h4 id="mesIpva">R$ 0,00</h4>
            </div>
            <div class="mensal-mini-card manut">
                <span>Guardado Manut.</span>
                <h4 id="mesManutencao">R$ 0,00</h4>
            </div>
            <div class="mensal-mini-card caix">
                <span>Guardado Caixinha</span>
                <h4 id="mesCaixinha">R$ 0,00</h4>
            </div>
        </div>

        <div class="mensal-footer-stats">
            <div class="result-item" style="margin-bottom: 8px;"><span>Dias Trabalhados:</span> <span id="mesDias" style="color:#fff; font-size: 1.1rem;">0 dias</span></div>
            <div class="result-item" style="margin-bottom: 0;"><span>Média Líquida Diária:</span> <span id="mesMediaDia" style="font-size: 1.1rem;">R$ 0,00</span></div>
        </div>
    </div>

    <!-- ABA HISTÓRICO -->
    <div id="tabHistorico" style="display: none;">
        <div class="section-title">Histórico de Lançamentos</div>
        <div id="listaHistorico" style="max-height: 450px; overflow-y: auto;"></div>
    </div>
</div>

<script>
    document.getElementById('dataRegistro').valueAsDate = new Date();

    let cronometroAtivo = false;
    let segundosTotais = 0;
    let intervalo = null;

    window.onload = function() {
        let config = JSON.parse(localStorage.getItem('configFixos')) || { parcela: 1375, seguro: 0, diasMes: 26 };
        document.getElementById('cfgParcelaMensal').value = config.parcela;
        document.getElementById('cfgSeguroMensal').value = config.seguro;
        document.getElementById('cfgDiasMes').value = config.diasMes;

        let dataHoje = new Date();
        let anoStr = dataHoje.getFullYear();
        let mesStr = String(dataHoje.getMonth() + 1).padStart(2, '0');
        document.getElementById('filtroMesAno').value = `${anoStr}-${mesStr}`;

        atualizarValoresAutomaticosDia();
        calcular();
    };

    window.onclick = function(event) {
        if (!event.target.matches('.menu-dots-btn')) {
            let dropdown = document.getElementById('menuDropdown');
            if (dropdown.classList.contains('show')) {
                dropdown.classList.remove('show');
            }
        }
    }

    function toggleMenuDropdown(event) {
        event.stopPropagation();
        document.getElementById('menuDropdown').classList.toggle('show');
    }

    function salvarConfiguracoes() {
        let parcela = parseFloat(document.getElementById('cfgParcelaMensal').value) || 0;
        let seguro = parseFloat(document.getElementById('cfgSeguroMensal').value) || 0;
        let diasMes = parseFloat(document.getElementById('cfgDiasMes').value) || 26;
        localStorage.setItem('configFixos', JSON.stringify({ parcela, seguro, diasMes }));
        atualizarValoresAutomaticosDia();
        calcular();
    }

    function atualizarValoresAutomaticosDia() {
        let config = JSON.parse(localStorage.getItem('configFixos')) || { parcela: 1375, seguro: 0, diasMes: 26 };
        let dias = config.diasMes > 0 ? config.diasMes : 26;
        let parcelaDia = config.parcela / dias;
        let seguroDia = config.seguro / dias;
        document.getElementById('parcelaCarro').value = parcelaDia.toFixed(2);
        document.getElementById('seguroCarro').value = seguroDia.toFixed(2);
    }

    function getCustosFixosAtuais() {
        let config = JSON.parse(localStorage.getItem('configFixos')) || { parcela: 1375, seguro: 0, diasMes: 26 };
        let dias = config.diasMes > 0 ? config.diasMes : 26;
        return (config.parcela / dias) + (config.seguro / dias);
    }

    function mudarTab(aba) {
        document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
        document.getElementById('tabDiario').style.display = 'none';
        document.getElementById('tabSemana').style.display = 'none';
        document.getElementById('tabMensal').style.display = 'none';
        document.getElementById('tabConfig').style.display = 'none';
        document.getElementById('tabHistorico').style.display = 'none';
        let tabManut = document.getElementById('tabManutencaoCarro');
        if(tabManut) tabManut.style.display = 'none';

        if(aba === 'diario') {
            document.getElementById('tabDiario').style.display = 'block';
            document.querySelectorAll('.tab-btn')[0].classList.add('active');
            atualizarValoresAutomaticosDia();
            calcular();
        } else if(aba === 'semana') {
            document.getElementById('tabSemana').style.display = 'block';
            document.querySelectorAll('.tab-btn')[1].classList.add('active');
            renderizarSemanal();
        } else if(aba === 'mensal') {
            document.getElementById('tabMensal').style.display = 'block';
            document.querySelectorAll('.tab-btn')[2].classList.add('active');
            renderizarMensal();
        } else if(aba === 'config') {
            document.getElementById('tabConfig').style.display = 'block';
            document.querySelectorAll('.tab-btn')[3].classList.add('active');
        } else if(aba === 'historico') {
            document.getElementById('tabHistorico').style.display = 'block';
            document.querySelectorAll('.tab-btn')[4].classList.add('active');
            renderizarHistorico();
        } else if(aba === 'manutencaoCarro') {
            if(tabManut) tabManut.style.display = 'block';
            renderizarManutencoesCarro();
        }
    }

    function salvarManutencaoCarro() {
        let servico = document.getElementById('manutServico').value.trim();
        let kmFeito = parseFloat(document.getElementById('manutKmFeito').value) || 0;
        let kmRefazer = parseFloat(document.getElementById('manutKmRefazer').value) || 0;
        let custo = parseFloat(document.getElementById('manutCusto').value) || 0;

        if(!servico) {
            alert("Por favor, digite o que foi mexido/serviço.");
            return;
        }

        let novaManut = {
            id: Date.now(),
            servico,
            kmFeito,
            kmRefazer,
            custo,
            dataRegistro: new Date().toLocaleDateString('pt-BR')
        };

        let lista = JSON.parse(localStorage.getItem('manutencoesCarro') || '[]');
        lista.push(novaManut);
        localStorage.setItem('manutencoesCarro', JSON.stringify(lista));

        document.getElementById('manutServico').value = '';
        document.getElementById('manutKmFeito').value = '';
        document.getElementById('manutKmRefazer').value = '';
        document.getElementById('manutCusto').value = '';

        renderizarManutencoesCarro();
        alert("Manutenção registada com sucesso!");
    }

    function renderizarManutencoesCarro() {
        let lista = JSON.parse(localStorage.getItem('manutencoesCarro') || '[]');
        let container = document.getElementById('listaManutencoesCarro');
        container.innerHTML = "";

        if(lista.length === 0) {
            container.innerHTML = "<p style='text-align:center; color:#888;'>Nenhuma manutenção registada.</p>";
            return;
        }

        let listaInvertida = lista.slice().reverse();
        listaInvertida.forEach((item) => {
            container.innerHTML += `
                <div class="historico-item" style="flex-direction: column; align-items: flex-start; gap: 4px;">
                    <div style="display: flex; width: 100%; justify-content: space-between;">
                        <strong style="color: var(--primary-color); font-size: 1.05rem;">${item.servico}</strong>
                        <button class="btn-sm btn-delete" onclick="deletarManutencaoCarro(${item.id})">Excluir</button>
                    </div>
                    <div style="font-size: 0.85rem; color: #ccc;">Data do registo: ${item.dataRegistro}</div>
                    <div style="display: flex; gap: 15px; font-size: 0.9rem; margin-top: 4px;">
                        <span>KM Feito: <strong>${item.kmFeito ? item.kmFeito + ' km' : 'N/A'}</strong></span>
                        <span>Refazer com: <strong style="color: var(--edit-color);">${item.kmRefazer ? item.kmRefazer + ' km' : 'N/A'}</strong></span>
                    </div>
                    ${item.custo > 0 ? `<div style="font-size: 0.85rem; color: var(--reserve-color);">Custo: R$ ${item.custo.toFixed(2)}</div>` : ''}
                </div>
            `;
        });
    }

    function deletarManutencaoCarro(id) {
        if(confirm("Deseja apagar este registo de manutenção?")) {
            let lista = JSON.parse(localStorage.getItem('manutencoesCarro') || '[]');
            lista = lista.filter(item => item.id !== id);
            localStorage.setItem('manutencoesCarro', JSON.stringify(lista));
            renderizarManutencoesCarro();
        }
    }

    function toggleCronometro() {
        const btn = document.getElementById('btnChrono');
        if (!cronometroAtivo) {
            cronometroAtivo = true;
            btn.innerText = "Parar";
            btn.className = "btn-chrono btn-stop";
            intervalo = setInterval(() => {
                segundosTotais++;
                document.getElementById('horasOnline').value = (segundosTotais / 3600).toFixed(2);
                calcular();
            }, 1000);
        } else {
            cronometroAtivo = false;
            btn.innerText = "Iniciar";
            btn.className = "btn-chrono btn-start";
            clearInterval(intervalo);
        }
    }

    function calcularCombustivelPorLitros() {
        let litros = parseFloat(document.getElementById('litros').value) || 0;
        let preco = parseFloat(document.getElementById('precoLitro').value) || 0;
        if(litros > 0 && preco > 0) {
            document.getElementById('valorAbastecido').value = (litros * preco).toFixed(2);
        }
        calcular();
    }

    function calcular() {
        let bruto = parseFloat(document.getElementById('bruto').value) || 0;
        let kmIni = parseFloat(document.getElementById('kmInicial').value) || 0;
        let kmFin = parseFloat(document.getElementById('kmFinal').value) || 0;
        let valAbast = parseFloat(document.getElementById('valorAbastecido').value) || 0;
        let gastos = parseFloat(document.getElementById('gastosRua').value) || 0;
        let horas = parseFloat(document.getElementById('horasOnline').value) || 0;
        
        let totalFixos = getCustosFixosAtuais();
        let resIpva = parseFloat(document.getElementById('reservaIpva').value) || 0;
        let resManut = parseFloat(document.getElementById('reservaManutencao').value) || 0;
        let resCaixinha = parseFloat(document.getElementById('reservaCaixinha').value) || 0;

        let kmRodados = kmFin > kmIni ? kmFin - kmIni : 0;
        let liquido = bruto - valAbast - totalFixos - gastos - resIpva - resManut - resCaixinha;
        let porHora = horas > 0 ? bruto / horas : 0;
        let porKm = kmRodados > 0 ? bruto / kmRodados : 0;

        document.getElementById('resKm').innerText = kmRodados + " km";
        document.getElementById('resCombustivel').innerText = "R$ " + valAbast.toFixed(2);
        document.getElementById('resCustosFixos').innerText = "R$ " + totalFixos.toFixed(2);
        document.getElementById('resGastosRua').innerText = "R$ " + gastos.toFixed(2);
        document.getElementById('resPorHora').innerText = "R$ " + porHora.toFixed(2) + " /h";
        document.getElementById('resPorKm').innerText = "R$ " + porKm.toFixed(2) + " /km";
        document.getElementById('resLiquido').innerText = "R$ " + liquido.toFixed(2);

        return { kmRodados, valAbast, totalFixos, gastos, liquido, porKm, porHora };
    }

    function salvarDia() {
        let data = document.getElementById('dataRegistro').value;
        let diaSemana = document.getElementById('diaSemana').value;
        let bruto = parseFloat(document.getElementById('bruto').value) || 0;
        let kmInicial = parseFloat(document.getElementById('kmInicial').value) || 0;
        let kmFinal = parseFloat(document.getElementById('kmFinal').value) || 0;
        let horas = parseFloat(document.getElementById('horasOnline').value) || 0;
        let valorAbastecido = parseFloat(document.getElementById('valorAbastecido').value) || 0;
        let gastosRua = parseFloat(document.getElementById('gastosRua').value) || 0;
        
        let config = JSON.parse(localStorage.getItem('configFixos')) || { parcela: 1375, seguro: 0, diasMes: 26 };
        let dias = config.diasMes > 0 ? config.diasMes : 26;
        let parcelaCarro = config.parcela / dias;
        let seguroCarro = config.seguro / dias;
        let totalFixos = parcelaCarro + seguroCarro;

        let reservaIpva = parseFloat(document.getElementById('reservaIpva').value) || 0;
        let reservaManutencao = parseFloat(document.getElementById('reservaManutencao').value) || 0;
        let reservaCaixinha = parseFloat(document.getElementById('reservaCaixinha').value) || 0;
        
        let kmRodados = kmFinal > kmInicial ? kmFinal - kmInicial : 0;
        let liquido = bruto - valorAbastecido - totalFixos - gastosRua - reservaIpva - reservaManutencao - reservaCaixinha;
        let porKm = kmRodados > 0 ? bruto / kmRodados : 0;
        let porHora = horas > 0 ? bruto / horas : 0;

        let registro = {
            data, diaSemana, bruto, kmInicial, kmFinal, kmRodados,
            horas, valorAbastecido, gastosRua, parcelaCarro, seguroCarro, totalFixos,
            reservaIpva, reservaManutencao, reservaCaixinha, liquido, porKm, porHora
        };

        let historico = JSON.parse(localStorage.getItem('historicoDias') || '[]');
        historico.push(registro);

        localStorage.setItem('historicoDias', JSON.stringify(historico));
        alert("Salvo com sucesso!");
        limparFormulario();
    }

    function limparFormulario() {
        document.getElementById('bruto').value = '';
        document.getElementById('kmInicial').value = '';
        document.getElementById('kmFinal').value = '';
        document.getElementById('horasOnline').value = '0.00';
        document.getElementById('valorAbastecido').value = '';
        document.getElementById('gastosRua').value = '';
        document.getElementById('dataRegistro').valueAsDate = new Date();
        calcular();
    }

    function getNumeroSemana(dataStr) {
        if(!dataStr) return "Semana Atual";
        let d = new Date(dataStr + 'T00:00:00');
        d.setHours(0, 0, 0, 0);
        d.setDate(d.getDate() + 4 - (d.getDay() || 7));
        let anoInicio = new Date(d.getFullYear(), 0, 1);
        let semanaNo = Math.ceil((((d - anoInicio) / 86400000) + 1) / 7);
        return `Semana ${semanaNo} (${d.getFullYear()})`;
    }

    function renderizarSemanal() {
        let historico = JSON.parse(localStorage.getItem('historicoDias') || '[]');
        let container = document.getElementById('listaSemanal');
        container.innerHTML = "";

        if(historico.length === 0) {
            container.innerHTML = "<p style='text-align:center; color:#888;'>Nenhum registo encontrado.</p>";
            return;
        }

        let semanas = {};
        historico.forEach((item, index) => {
            let sem = getNumeroSemana(item.data);
            if(!semanas[sem]) semanas[sem] = [];
            semanas[sem].push({...item, originalIndex: index});
        });

        let chavesSemanas = Object.keys(semanas);
        let ultimaSemana = chavesSemanas[chavesSemanas.length - 1];
        let itensSemana = semanas[ultimaSemana];

        const abrevDias = [
            { nome: 'Segunda-feira', abrev: 'seg' },
            { nome: 'Terça-feira', abrev: 'ter' },
            { nome: 'Quarta-feira', abrev: 'qua' },
            { nome: 'Quinta-feira', abrev: 'qui' },
            { nome: 'Sexta-feira', abrev: 'sex' },
            { nome: 'Sábado', abrev: 'sáb' },
            { nome: 'Domingo', abrev: 'dom' }
        ];

        let totalBruto = itensSemana.reduce((acc, curr) => acc + curr.bruto, 0);
        let totalLiquido = itensSemana.reduce((acc, curr) => acc + curr.liquido, 0);
        let totalKmSem = itensSemana.reduce((acc, curr) => acc + (curr.kmRodados || 0), 0);
        let totalHorasSem = itensSemana.reduce((acc, curr) => acc + (curr.horas || 0), 0);
        
        let valorKmSemana = totalKmSem > 0 ? totalBruto / totalKmSem : 0;
        let valorHrSemana = totalHorasSem > 0 ? totalBruto / totalHorasSem : 0;

        let totalIpvaSem = itensSemana.reduce((acc, curr) => acc + (curr.reservaIpva || 0), 0);
        let totalManutSem = itensSemana.reduce((acc, curr) => acc + (curr.reservaManutencao || 0), 0);
        let totalCaixinhaSem = itensSemana.reduce((acc, curr) => acc + (curr.reservaCaixinha || 0), 0);
        let maxBruto = Math.max(...itensSemana.map(i => i.bruto), 1);

        let mapaDias = {};
        itensSemana.forEach(i => { mapaDias[i.diaSemana] = i; });

        let chartHtml = '';
        abrevDias.forEach(d => {
            let dadoDia = mapaDias[d.nome];
            let valBruto = dadoDia ? dadoDia.bruto : 0;
            let alturaPx = maxBruto > 0 && valBruto > 0 ? Math.round((valBruto / maxBruto) * 70) : 10;
            if(valBruto > 0 && alturaPx < 10) alturaPx = 10;
            let activeClass = valBruto > 0 ? 'active' : '';
            let clickAction = dadoDia ? `abrirEdicaoSemanal('${ultimaSemana}', ${dadoDia.originalIndex})` : `alert('Nenhum registo para ${d.nome} nesta semana.')`;

            chartHtml += `
                <div class="chart-col" onclick="${clickAction}" title="Editar ${d.nome}">
                    <div class="chart-val">${valBruto > 0 ? 'R$' + valBruto.toFixed(0) : ''}</div>
                    <div class="chart-bar-wrapper">
                        <div class="chart-bar ${activeClass}" style="height: ${alturaPx}px;"></div>
                    </div>
                    <div class="chart-day">${d.abrev}</div>
                </div>
            `;
        });

        let semIdSafe = ultimaSemana.replace(/[^a-zA-Z0-9]/g, '_');

        container.innerHTML = `
            <div class="card-box" id="cardSemana_${semIdSafe}">
                <div style="font-size: 0.9rem; color: #aaa;">${ultimaSemana}</div>
                <div style="font-size: 1.3rem; font-weight: bold; color: #fff; margin-top: 4px;">Bruto: R$ ${totalBruto.toFixed(2)}</div>
                
                <div class="chart-container-semana">${chartHtml}</div>

                <div id="painelEdicao_${semIdSafe}"></div>
                
                <div style="margin-top: 12px;">
                    <div class="sobra-livre-box" style="margin-bottom: 10px;">
                        <div style="font-size: 0.8rem; color: #ccc; text-transform: uppercase;">Sobra Livre (Disponível)</div>
                        <div class="sobra-livre-val">R$ ${totalLiquido.toFixed(2)}</div>
                    </div>

                    <div class="mensal-grid">
                        <div class="mensal-mini-card km">
                            <span>Total KM Rodados</span>
                            <h4>${totalKmSem} km</h4>
                        </div>
                        <div class="mensal-mini-card vkm">
                            <span>Fat. por KM</span>
                            <h4>R$ ${valorKmSemana.toFixed(2)}</h4>
                        </div>
                        <div class="mensal-mini-card vhr">
                            <span>Fat. por Hora</span>
                            <h4>R$ ${valorHrSemana.toFixed(2)}</h4>
                        </div>
                        <div class="mensal-mini-card ipva">
                            <span>Guardado IPVA</span>
                            <h4>R$ ${totalIpvaSem.toFixed(2)}</h4>
                        </div>
                        <div class="mensal-mini-card manut">
                            <span>Guardado Manut.</span>
                            <h4>R$ ${totalManutSem.toFixed(2)}</h4>
                        </div>
                        <div class="mensal-mini-card caix">
                            <span>Guardado Caixinha</span>
                            <h4>R$ ${totalCaixinhaSem.toFixed(2)}</h4>
                        </div>
                    </div>
                </div>
            </div>
        `;
    }

    function abrirEdicaoSemanal(sem, index) {
        let historico = JSON.parse(localStorage.getItem('historicoDias') || '[]');
        let item = historico[index];
        let semIdSafe = sem.replace(/[^a-zA-Z0-9]/g, '_');
        let container = document.getElementById('painelEdicao_' + semIdSafe);
        
        container.innerHTML = gerarHtmlEdicaoDia(index, item, 'fecharEdicaoSemanal');
        container.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
    }

    function fecharEdicaoSemanal() {
        renderizarSemanal();
    }

    function renderizarMensal() {
        let valorMesAno = document.getElementById('filtroMesAno').value;
        if (!valorMesAno) return;

        let [anoSel, mesSel] = valorMesAno.split('-').map(Number);
        let historico = JSON.parse(localStorage.getItem('historicoDias') || '[]');

        let historicoMes = historico.map((item, originalIndex) => ({ ...item, originalIndex })).filter(item => {
            if (!item.data) return false;
            let [anoItem, mesItem] = item.data.split('-').map(Number);
            return anoItem === anoSel && mesItem === mesSel;
        });

        let totalBruto = historicoMes.reduce((acc, curr) => acc + curr.bruto, 0);
        let totalLiquido = historicoMes.reduce((acc, curr) => acc + curr.liquido, 0);
        let totalKmMes = historicoMes.reduce((acc, curr) => acc + (curr.kmRodados || 0), 0);
        let totalHorasMes = historicoMes.reduce((acc, curr) => acc + (curr.horas || 0), 0);
        
        let valorKmMes = totalKmMes > 0 ? totalBruto / totalKmMes : 0;
        let valorHrMes = totalHorasMes > 0 ? totalBruto / totalHorasMes : 0;

        let totalIpvaMes = historicoMes.reduce((acc, curr) => acc + (curr.reservaIpva || 0), 0);
        let totalManutMes = historicoMes.reduce((acc, curr) => acc + (curr.reservaManutencao || 0), 0);
        let totalCaixinhaMes = historicoMes.reduce((acc, curr) => acc + (curr.reservaCaixinha || 0), 0);

        let diasQtd = historicoMes.length;
        let mediaDia = diasQtd > 0 ? totalLiquido / diasQtd : 0;

        document.getElementById('mesBrutoGrande').innerText = "R$ " + totalBruto.toFixed(2);
        document.getElementById('mesLiquido').innerText = "R$ " + totalLiquido.toFixed(2);
        document.getElementById('mesKmTotal').innerText = totalKmMes + " km";
        document.getElementById('mesValorKm').innerText = "R$ " + valorKmMes.toFixed(2) + " /km";
        document.getElementById('mesValorHr').innerText = "R$ " + valorHrMes.toFixed(2) + " /h";
        document.getElementById('mesIpva').innerText = "R$ " + totalIpvaMes.toFixed(2);
        document.getElementById('mesManutencao').innerText = "R$ " + totalManutMes.toFixed(2);
        document.getElementById('mesCaixinha').innerText = "R$ " + totalCaixinhaMes.toFixed(2);
        document.getElementById('mesDias').innerText = diasQtd + " dias";
        document.getElementById('mesMediaDia').innerText = "R$ " + mediaDia.toFixed(2);

        let calendarContainer = document.getElementById('calendarDaysContainer');
        calendarContainer.innerHTML = "";

        let primeiroDiaDoMes = new Date(anoSel, mesSel - 1, 1);
        let diaSemanaInicio = primeiroDiaDoMes.getDay();
        let offsetDias = (diaSemanaInicio === 0) ? 6 : diaSemanaInicio - 1;

        let totalDiasNoMes = new Date(anoSel, mesSel, 0).getDate();

        let mapaHistoricoPorData = {};
        historicoMes.forEach((item) => {
            mapaHistoricoPorData[item.data] = item;
        });

        for (let i = 0; i < offsetDias; i++) {
            calendarContainer.innerHTML += `<div class="calendar-day-cell empty"></div>`;
        }

        for (let dia = 1; dia <= totalDiasNoMes; dia++) {
            let diaStr = String(dia).padStart(2, '0');
            let mesStr = String(mesSel).padStart(2, '0');
            let dataChave = `${anoSel}-${mesStr}-${diaStr}`;

            let registroDia = mapaHistoricoPorData[dataChave];
            let temTrabalho = registroDia && registroDia.bruto > 0;
            let valBruto = temTrabalho ? registroDia.bruto : 0;

            let workedClass = temTrabalho ? 'worked' : '';
            let clickAction = temTrabalho ? `abrirEdicaoMensal(${registroDia.originalIndex})` : `alert('Dia ${dia}/${mesStr}: Folga ou sem registos.')`;
            let valDisplay = temTrabalho ? `R$${valBruto.toFixed(0)}` : '';

            calendarContainer.innerHTML += `
                <div class="calendar-day-cell ${workedClass}" onclick="${clickAction}" title="${dataChave}">
                    <div class="cal-day-num">${dia}</div>
                    <div class="cal-day-val">${valDisplay}</div>
                </div>
            `;
        }
    }

    function abrirEdicaoMensal(index) {
        let historico = JSON.parse(localStorage.getItem('historicoDias') || '[]');
        let item = historico[index];
        let container = document.getElementById('painelEdicaoMensal');
        
        container.innerHTML = gerarHtmlEdicaoDia(index, item, 'fecharEdicaoMensal');
        container.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
    }

    function fecharEdicaoMensal() {
        document.getElementById('painelEdicaoMensal').innerHTML = "";
        renderizarMensal();
    }

    function gerarHtmlEdicaoDia(index, item, callbackFechar) {
        return `
            <div class="dia-semana-edit-card">
                <div style="font-size: 1rem; font-weight: bold; color: var(--edit-color); margin-bottom: 8px; text-align: center;">Editando: ${item.diaSemana} (${item.data})</div>
                
                <div style="display: flex; gap: 8px;">
                    <div class="form-group" style="flex:1;">
                        <label style="font-size:0.8rem;">Data</label>
                        <input type="date" id="EdData_${index}" value="${item.data}">
                    </div>
                    <div class="form-group" style="flex:1;">
                        <label style="font-size:0.8rem;">Dia da Semana</label>
                        <select id="EdDiaSemana_${index}">
                            <option value="Segunda-feira" ${item.diaSemana==='Segunda-feira'?'selected':''}>Segunda</option>
                            <option value="Terça-feira" ${item.diaSemana==='Terça-feira'?'selected':''}>Terça</option>
                            <option value="Quarta-feira" ${item.diaSemana==='Quarta-feira'?'selected':''}>Quarta</option>
                            <option value="Quinta-feira" ${item.diaSemana==='Quinta-feira'?'selected':''}>Quinta</option>
                            <option value="Sexta-feira" ${item.diaSemana==='Sexta-feira'?'selected':''}>Sexta</option>
                            <option value="Sábado" ${item.diaSemana==='Sábado'?'selected':''}>Sábado</option>
                            <option value="Domingo" ${item.diaSemana==='Domingo'?'selected':''}>Domingo</option>
                        </select>
                    </div>
                </div>

                <div style="display: flex; gap: 8px;">
                    <div class="form-group" style="flex:1;">
                        <label style="font-size:0.8rem;">Faturamento Bruto (R$)</label>
                        <input type="number" id="EdBruto_${index}" value="${item.bruto}">
                    </div>
                    <div class="form-group" style="flex:1;">
                        <label style="font-size:0.8rem;">Horas Online</label>
                        <input type="number" id="EdHoras_${index}" value="${item.horas}">
                    </div>
                </div>

                <div style="display: flex; gap: 8px;">
                    <div class="form-group" style="flex:1;">
                        <label style="font-size:0.8rem;">KM Inicial</label>
                        <input type="number" id="EdKmIni_${index}" value="${item.kmInicial || 0}">
                    </div>
                    <div class="form-group" style="flex:1;">
                        <label style="font-size:0.8rem;">KM Final</label>
                        <input type="number" id="EdKmFin_${index}" value="${item.kmFinal || 0}">
                    </div>
                </div>

                <div style="display: flex; gap: 8px;">
                    <div class="form-group" style="flex:1;">
                        <label style="font-size:0.8rem;">Valor Abastecido (R$)</label>
                        <input type="number" id="EdAbast_${index}" value="${item.valorAbastecido}">
                    </div>
                    <div class="form-group" style="flex:1;">
                        <label style="font-size:0.8rem;">Gastos na Rua (R$)</label>
                        <input type="number" id="EdGastos_${index}" value="${item.gastosRua}">
                    </div>
                </div>

                <div style="display: flex; gap: 8px;">
                    <div class="form-group" style="flex:1;">
                        <label style="font-size:0.8rem;">Reserva IPVA (R$)</label>
                        <input type="number" id="EdIpva_${index}" value="${item.reservaIpva || 0}">
                    </div>
                    <div class="form-group" style="flex:1;">
                        <label style="font-size:0.8rem;">Reserva Manut. (R$)</label>
                        <input type="number" id="EdManut_${index}" value="${item.reservaManutencao || 0}">
                    </div>
                    <div class="form-group" style="flex:1;">
                        <label style="font-size:0.8rem;">Caixinha (R$)</label>
                        <input type="number" id="EdCaixinha_${index}" value="${item.reservaCaixinha || 0}">
                    </div>
                </div>

                <div style="display: flex; gap: 8px; margin-top: 8px;">
                    <button class="btn-sm btn-edit" style="flex:1; padding:10px;" onclick="salvarEdicaoDia(${index}, '${callbackFechar}')">Salvar Alterações</button>
                    <button class="btn-sm btn-delete" style="padding:10px;" onclick="${callbackFechar}()">Cancelar</button>
                </div>
            </div>
        `;
    }

    function salvarEdicaoDia(index, callbackFecharName) {
        let historico = JSON.parse(localStorage.getItem('historicoDias') || '[]');
        
        let novaData = document.getElementById(`EdData_${index}`).value;
        let novoDiaSemana = document.getElementById(`EdDiaSemana_${index}`).value;
        let novoBruto = parseFloat(document.getElementById(`EdBruto_${index}`).value) || 0;
        let novasHoras = parseFloat(document.getElementById(`EdHoras_${index}`).value) || 0;
        let novoKmIni = parseFloat(document.getElementById(`EdKmIni_${index}`).value) || 0;
        let novoKmFin = parseFloat(document.getElementById(`EdKmFin_${index}`).value) || 0;
        let novoAbast = parseFloat(document.getElementById(`EdAbast_${index}`).value) || 0;
        let novoGastos = parseFloat(document.getElementById(`EdGastos_${index}`).value) || 0;
        let novoIpva = parseFloat(document.getElementById(`EdIpva_${index}`).value) || 0;
        let novoManut = parseFloat(document.getElementById(`EdManut_${index}`).value) || 0;
        let novoCaixinha = parseFloat(document.getElementById(`EdCaixinha_${index}`).value) || 0;

        let kmRodados = novoKmFin > novoKmIni ? novoKmFin - novoKmIni : 0;
        let totalFixos = historico[index].totalFixos || getCustosFixosAtuais();
        let liquido = novoBruto - novoAbast - totalFixos - novoGastos - novoIpva - novoManut - novoCaixinha;
        let porKm = kmRodados > 0 ? novoBruto / kmRodados : 0;
        let porHora = novasHoras > 0 ? novoBruto / novasHoras : 0;

        historico[index].data = novaData;
        historico[index].diaSemana = novoDiaSemana;
        historico[index].bruto = novoBruto;
        historico[index].horas = novasHoras;
        historico[index].kmInicial = novoKmIni;
        historico[index].kmFinal = novoKmFin;
        historico[index].kmRodados = kmRodados;
        historico[index].valorAbastecido = novoAbast;
        historico[index].gastosRua = novoGastos;
        historico[index].reservaIpva = novoIpva;
        historico[index].reservaManutencao = novoManut;
        historico[index].reservaCaixinha = novoCaixinha;
        historico[index].liquido = liquido;
        historico[index].porKm = porKm;
        historico[index].porHora = porHora;

        localStorage.setItem('historicoDias', JSON.stringify(historico));
        
        if(callbackFecharName === 'fecharEdicaoSemanal') {
            fecharEdicaoSemanal();
        } else {
            fecharEdicaoMensal();
        }
    }

    function renderizarHistorico() {
        let historico = JSON.parse(localStorage.getItem('historicoDias') || '[]');
        let container = document.getElementById('listaHistorico');
        container.innerHTML = "";
        if(historico.length === 0) {
            container.innerHTML = "<p style='text-align:center; color:#888;'>Nenhum registo.</p>";
            return;
        }
        let historicoInvertido = historico.slice().reverse();
        historicoInvertido.forEach((item, idx) => {
            let realIdx = historico.length - 1 - idx;
            container.innerHTML += `
                <div class="historico-item">
                    <div>
                        <div style="font-size: 0.85rem; color: #ccc;">${item.data} - <strong>${item.diaSemana}</strong></div>
                        <div style="font-size: 1rem; color: var(--primary-color); font-weight: bold;">Livre: R$ ${item.liquido.toFixed(2)}</div>
                    </div>
                    <div>
                        <button class="btn-sm btn-delete" onclick="deletarRegistro(${realIdx})">Excluir</button>
                    </div>
                </div>
            `;
        });
    }

    function deletarRegistro(index) {
        if(confirm("Excluir este dia do histórico?")) {
            let historico = JSON.parse(localStorage.getItem('historicoDias') || '[]');
            historico.splice(index, 1);
            localStorage.setItem('historicoDias', JSON.stringify(historico));
            renderizarHistorico();
            renderizarMensal();
        }
    }
</script>

</body>
</html>
