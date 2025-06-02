<!DOCTYPE html>
<html>
<head>
    <title>国家模拟器 - 终极版</title>
    <style>
        :root {
            --primary-color: #3498db;
            --secondary-color: #2ecc71;
            --danger-color: #e74c3c;
            --warning-color: #f39c12;
            --dark-color: #2c3e50;
            --light-color: #ecf0f1;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #f5f7fa;
            color: #34495e;
            margin: 0;
            padding: 0;
        }
        #gameContainer {
            max-width: 1200px;
            margin: 0 auto;
            background: white;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            padding: 25px;
            position: relative;
        }
        #countryHeader {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 2px solid #eee;
            padding-bottom: 20px;
            margin-bottom: 25px;
        }
        #countryInfo {
            flex: 1;
        }
        #countryName {
            font-size: 32px;
            font-weight: bold;
            color: var(--dark-color);
            margin: 0;
        }
        #governmentType {
            font-size: 18px;
            color: #7f8c8d;
            margin: 5px 0;
        }
        #countryStats {
            display: flex;
            gap: 15px;
        }
        .countryStat {
            text-align: center;
        }
        .countryStat .label {
            font-size: 14px;
            color: #7f8c8d;
        }
        .countryStat .value {
            font-size: 20px;
            font-weight: bold;
        }
        #countryFlag {
            width: 150px;
            height: 100px;
            background: #ddd;
            border: 2px solid #ccc;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .dashboard {
            display: grid;
            grid-template-columns: 2fr 1fr;
            gap: 25px;
            margin-bottom: 30px;
        }
        .mainPanel {
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            padding: 20px;
        }
        .sidePanel {
            display: flex;
            flex-direction: column;
            gap: 25px;
        }
        .panel {
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.05);
            padding: 20px;
        }
        .panelTitle {
            font-size: 20px;
            margin-top: 0;
            margin-bottom: 20px;
            color: var(--dark-color);
            border-bottom: 1px solid #eee;
            padding-bottom: 10px;
        }
        .tabs {
            display: flex;
            border-bottom: 1px solid #eee;
            margin-bottom: 20px;
        }
        .tab {
            padding: 10px 20px;
            cursor: pointer;
            border-bottom: 3px solid transparent;
            transition: all 0.3s;
        }
        .tab:hover {
            background: #f8f9fa;
        }
        .tab.active {
            border-bottom-color: var(--primary-color);
            font-weight: bold;
            color: var(--primary-color);
        }
        .policyCard {
            background: #f8f9fa;
            border-radius: 6px;
            padding: 15px;
            margin-bottom: 15px;
            border-left: 4px solid var(--primary-color);
            transition: all 0.3s;
        }
        .policyCard:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        .policyHeader {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 10px;
        }
        .policyName {
            font-size: 18px;
            font-weight: bold;
            margin: 0;
            color: var(--dark-color);
        }
        .policyCost {
            background: var(--primary-color);
            color: white;
            padding: 3px 10px;
            border-radius: 20px;
            font-size: 14px;
        }
        .policyDesc {
            color: #7f8c8d;
            margin: 10px 0;
        }
        .policyEffects {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin: 15px 0;
        }
        .effect {
            display: flex;
            align-items: center;
            font-size: 14px;
            padding: 3px 10px;
            border-radius: 20px;
            background: #ecf0f1;
        }
        .effect.positive {
            background: rgba(46, 204, 113, 0.1);
            color: var(--secondary-color);
        }
        .effect.negative {
            background: rgba(231, 76, 60, 0.1);
            color: var(--danger-color);
        }
        .effect.neutral {
            background: rgba(52, 152, 219, 0.1);
            color: var(--primary-color);
        }
        .policyActions {
            display: flex;
            justify-content: flex-end;
            gap: 10px;
        }
        .btn {
            padding: 8px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
        }
        .btn-primary {
            background: var(--primary-color);
            color: white;
        }
        .btn-primary:hover {
            background: #2980b9;
        }
        .btn-secondary {
            background: var(--secondary-color);
            color: white;
        }
        .btn-secondary:hover {
            background: #27ae60;
        }
        .btn-danger {
            background: var(--danger-color);
            color: white;
        }
        .btn-danger:hover {
            background: #c0392b;
        }
        .btn:disabled {
            background: #bdc3c7;
            cursor: not-allowed;
        }
        .resourceMeter {
            margin-bottom: 15px;
        }
        .meterHeader {
            display: flex;
            justify-content: space-between;
            margin-bottom: 5px;
        }
        .meterLabel {
            font-weight: bold;
        }
        .meterValue {
            font-weight: bold;
        }
        .meterBar {
            height: 10px;
            background: #ecf0f1;
            border-radius: 5px;
            overflow: hidden;
        }
        .meterFill {
            height: 100%;
            border-radius: 5px;
            transition: width 0.5s;
        }
        .meterFill.gdp {
            background: var(--primary-color);
        }
        .meterFill.approval {
            background: var(--secondary-color);
        }
        .meterFill.treasury {
            background: var(--warning-color);
        }
        .meterFill.military {
            background: var(--danger-color);
        }
        .newsItem {
            padding: 15px;
            border-bottom: 1px solid #eee;
            transition: all 0.3s;
        }
        .newsItem:hover {
            background: #f8f9fa;
        }
        .newsItem:last-child {
            border-bottom: none;
        }
        .newsTitle {
            font-weight: bold;
            margin: 0 0 5px 0;
        }
        .newsDate {
            font-size: 12px;
            color: #7f8c8d;
            margin-bottom: 5px;
        }
        .newsContent {
            margin: 0;
            color: #7f8c8d;
        }
        .timeControls {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-top: 30px;
        }
        .timeBtn {
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s;
        }
        .timeBtn.active {
            background: var(--primary-color);
            color: white;
        }
        #currentDate {
            text-align: center;
            font-size: 20px;
            margin: 20px 0;
            color: var(--dark-color);
            font-weight: bold;
        }
        .achievement {
            display: flex;
            align-items: center;
            padding: 10px;
            margin-bottom: 10px;
            background: #f8f9fa;
            border-radius: 6px;
        }
        .achievementIcon {
            width: 40px;
            height: 40px;
            background: var(--primary-color);
            color: white;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 15px;
            font-size: 20px;
        }
        .achievementInfo {
            flex: 1;
        }
        .achievementTitle {
            font-weight: bold;
            margin: 0 0 5px 0;
        }
        .achievementDesc {
            font-size: 14px;
            color: #7f8c8d;
            margin: 0;
        }
        #eventModal {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.7);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.3s;
        }
        #eventModal.active {
            opacity: 1;
            pointer-events: all;
        }
        .modalContent {
            background: white;
            border-radius: 10px;
            width: 80%;
            max-width: 600px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            transform: translateY(20px);
            transition: transform 0.3s;
        }
        #eventModal.active .modalContent {
            transform: translateY(0);
        }
        .modalHeader {
            background: var(--dark-color);
            color: white;
            padding: 20px;
        }
        .modalTitle {
            margin: 0;
            font-size: 24px;
        }
        .modalBody {
            padding: 20px;
        }
        .modalText {
            margin: 0 0 20px 0;
            line-height: 1.6;
        }
        .modalImage {
            width: 100%;
            height: 200px;
            background: #ddd;
            margin-bottom: 20px;
            background-size: cover;
            background-position: center;
        }
        .modalChoices {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .choiceBtn {
            padding: 12px;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            text-align: left;
            transition: all 0.3s;
            background: #f8f9fa;
        }
        .choiceBtn:hover {
            background: var(--primary-color);
            color: white;
        }
        .techTree {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 15px;
        }
        .techCard {
            background: white;
            border-radius: 8px;
            padding: 15px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            border: 1px solid #eee;
            transition: all 0.3s;
        }
        .techCard:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
        }
        .techCard.researched {
            border-left: 4px solid var(--secondary-color);
        }
        .techCard.available {
            border-left: 4px solid var(--primary-color);
        }
        .techCard.locked {
            opacity: 0.6;
            border-left: 4px solid #bdc3c7;
        }
        .techName {
            font-weight: bold;
            margin: 0 0 10px 0;
        }
        .techDesc {
            font-size: 14px;
            color: #7f8c8d;
            margin: 0 0 15px 0;
        }
        .techRequirements {
            font-size: 12px;
            color: #7f8c8d;
            margin: 0 0 15px 0;
        }
        .techEffects {
            font-size: 14px;
            margin: 0 0 15px 0;
        }
        .techBtn {
            width: 100%;
            padding: 8px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: bold;
        }
        .techBtn.research {
            background: var(--primary-color);
            color: white;
        }
        .techBtn.researched {
            background: var(--secondary-color);
            color: white;
        }
        .techBtn.locked {
            background: #bdc3c7;
            cursor: not-allowed;
        }
    </style>
</head>
<body>
    <div id="gameContainer">
        <div id="countryHeader">
            <div id="countryInfo">
                <h1 id="countryName">新共和国</h1>
                <div id="governmentType">民主共和制</div>
                <div id="countryStats">
                    <div class="countryStat">
                        <div class="label">国际排名</div>
                        <div class="value">#42</div>
                    </div>
                    <div class="countryStat">
                        <div class="label">执政时间</div>
                        <div class="value">1年</div>
                    </div>
                    <div class="countryStat">
                        <div class="label">难度</div>
                        <div class="value">中等</div>
                    </div>
                </div>
            </div>
            <div id="countryFlag"></div>
        </div>

        <div id="currentDate">2023年1月</div>

        <div class="dashboard">
            <div class="mainPanel">
                <div class="tabs">
                    <div class="tab active" data-tab="policies">国家政策</div>
                    <div class="tab" data-tab="tech">科技发展</div>
                    <div class="tab" data-tab="diplomacy">外交关系</div>
                </div>

                <div id="policiesTab" class="tabContent active">
                    <div class="policyCategory">
                        <h3>经济政策</h3>
                        <div class="policyCard">
                            <div class="policyHeader">
                                <h4 class="policyName">提高企业所得税</h4>
                                <span class="policyCost">$0</span>
                            </div>
                            <p class="policyDesc">将企业所得税从20%提高到25%，增加政府财政收入但可能影响企业投资。</p>
                            <div class="policyEffects">
                                <span class="effect positive">+ 国库收入</span>
                                <span class="effect negative">- 企业满意度</span>
                                <span class="effect negative">- GDP增长</span>
                            </div>
                            <div class="policyActions">
                                <button class="btn btn-primary">实施政策</button>
                                <button class="btn">详情</button>
                            </div>
                        </div>

                        <div class="policyCard">
                            <div class="policyHeader">
                                <h4 class="policyName">基础设施建设计划</h4>
                                <span class="policyCost">$50亿</span>
                            </div>
                            <p class="policyDesc">投资$50亿用于道路、桥梁和公共交通建设，创造就业机会并促进经济增长。</p>
                            <div class="policyEffects">
                                <span class="effect negative">- 国库资金</span>
                                <span class="effect positive">+ 就业率</span>
                                <span class="effect positive">+ GDP增长</span>
                                <span class="effect positive">+ 支持率</span>
                            </div>
                            <div class="policyActions">
                                <button class="btn btn-primary">实施政策</button>
                                <button class="btn">详情</button>
                            </div>
                        </div>
                    </div>
                </div>

                <div id="techTab" class="tabContent">
                    <div class="techTree">
                        <div class="techCard available">
                            <h4 class="techName">可再生能源技术</h4>
                            <p class="techDesc">开发太阳能和风能技术，减少对化石燃料的依赖。</p>
                            <p class="techRequirements">需要: 基础科研能力</p>
                            <p class="techEffects">效果: 能源独立+20%, 污染-15%, GDP+5%</p>
                            <button class="techBtn research">研发 (3年)</button>
                        </div>

                        <div class="techCard locked">
                            <h4 class="techName">高速铁路网络</h4>
                            <p class="techDesc">建设全国高速铁路系统，提高运输效率。</p>
                            <p class="techRequirements">需要: 基础设施投资</p>
                            <p class="techEffects">效果: 交通效率+30%, GDP+8%</p>
                            <button class="techBtn locked">需要先决条件</button>
                        </div>
                    </div>
                </div>
            </div>

            <div class="sidePanel">
                <div class="panel">
                    <h3 class="panelTitle">国家概况</h3>
                    <div class="resourceMeter">
                        <div class="meterHeader">
                            <span class="meterLabel">GDP</span>
                            <span class="meterValue">$1.2万亿</span>
                        </div>
                        <div class="meterBar">
                            <div class="meterFill gdp" style="width: 65%"></div>
                        </div>
                    </div>
                    <div class="resourceMeter">
                        <div class="meterHeader">
                            <span class="meterLabel">支持率</span>
                            <span class="meterValue">62%</span>
                        </div>
                        <div class="meterBar">
                            <div class="meterFill approval" style="width: 62%"></div>
                        </div>
                    </div>
                    <div class="resourceMeter">
                        <div class="meterHeader">
                            <span class="meterLabel">国库</span>
                            <span class="meterValue">$450亿</span>
                        </div>
                        <div class="meterBar">
                            <div class="meterFill treasury" style="width: 45%"></div>
                        </div>
                    </div>
                    <div class="resourceMeter">
                        <div class="meterHeader">
                            <span class="meterLabel">军事实力</span>
                            <span class="meterValue">中等</span>
                        </div>
                        <div class="meterBar">
                            <div class="meterFill military" style="width: 50%"></div>
                        </div>
                    </div>
                </div>

                <div class="panel">
                    <h3 class="panelTitle">新闻动态</h3>
                    <div class="newsItem">
                        <div class="newsDate">2023年1月15日</div>
                        <h5 class="newsTitle">全球经济论坛发布年度报告</h5>
                        <p class="newsContent">我国经济排名上升2位，专家预测今年GDP增长率为2.3%。</p>
                    </div>
                    <div class="newsItem">
                        <div class="newsDate">2023年1月10日</div>
                        <h5 class="newsTitle">反对党批评政府开支计划</h5>
                        <p class="newsContent">反对党领袖称基础设施投资计划将导致财政赤字扩大。</p>
                    </div>
                </div>
            </div>
        </div>

        <div class="timeControls">
            <button class="timeBtn active">暂停</button>
            <button class="timeBtn">正常</button>
            <button class="timeBtn">快速</button>
            <button class="timeBtn">超速</button>
        </div>
    </div>

    <div id="eventModal">
        <div class="modalContent">
            <div class="modalHeader">
                <h3 class="modalTitle">重大事件</h3>
            </div>
            <div class="modalBody">
                <div class="modalImage"></div>
                <p class="modalText">全球金融市场动荡导致经济衰退开始影响我国。出口下降，失业率上升。</p>
                <div class="modalChoices">
                    <button class="choiceBtn">实施经济刺激计划 (国库-$80亿, GDP+1.5%, 支持率+3%)</button>
                    <button class="choiceBtn">坚持财政紧缩政策 (GDP-1%, 支持率-10%, 国库+30亿)</button>
                    <button class="choiceBtn">寻求国际援助 (外交关系-5, GDP+0.5%, 支持率-3%)</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // 游戏状态
        const gameState = {
            date: new Date(2023, 0, 1),
            stats: {
                gdp: 1200, // 十亿美元
                gdpGrowth: 2.3,
                population: 42.5, // 百万
                populationGrowth: 0.8,
                approval: 62,
                treasury: 45, // 十亿美元
                inflation: 2.1,
                unemployment: 5.4,
                militaryPower: 50,
                foreignRelations: 60,
                education: 65,
                healthcare: 70,
                infrastructure: 60,
                environment: 55,
                corruption: 30,
                techLevel: 40
            },
            policies: [],
            technologies: [],
            timeSpeed: 0, // 0 = 暂停, 1 = 正常, 2 = 快速, 3 = 超速
            eventCooldown: 0,
            relations: {
                neighbor1: { name: "北方联邦", relation: 65 },
                neighbor2: { name: "南方联盟", relation: 45 },
                superpower1: { name: "西方帝国", relation: 70 },
                superpower2: { name: "东方共和国", relation: 55 }
            },
            achievements: []
        };

        // 政策数据
        const policies = {
            economy: [
                {
                    id: "tax_increase",
                    name: "提高企业所得税",
                    description: "将企业所得税从20%提高到25%，增加政府财政收入但可能影响企业投资。",
                    cost: 0,
                    effects: {
                        treasury: 8,
                        corporateSatisfaction: -10,
                        gdpGrowth: -0.5
                    },
                    requirements: []
                },
                {
                    id: "infrastructure",
                    name: "基础设施建设计划",
                    description: "投资$50亿用于道路、桥梁和公共交通建设，创造就业机会并促进经济增长。",
                    cost: 5,
                    effects: {
                        treasury: -5,
                        employment: 2,
                        gdpGrowth: 0.8,
                        approval: 5,
                        infrastructure: 10
                    },
                    requirements: []
                }
            ],
            social: [
                {
                    id: "healthcare",
                    name: "全民医疗改革",
                    description: "建立覆盖所有公民的公共医疗系统，提高全民健康水平。",
                    cost: 7,
                    effects: {
                        treasury: -7,
                        approval: 8,
                        populationGrowth: 0.3,
                        healthcare: 15
                    },
                    requirements: []
                }
            ]
        };

        // 科技数据
        const technologies = [
            {
                id: "renewable",
                name: "可再生能源技术",
                description: "开发太阳能和风能技术，减少对化石燃料的依赖。",
                researchTime: 36, // 月份
                effects: {
                    energyIndependence: 20,
                    pollution: -15,
                    gdpGrowth: 0.5
                },
                requirements: {
                    techLevel: 40
                },
                researched: false
            }
        ];

        // 事件数据
        const events = [
            {
                id: "economic_crisis",
                title: "经济危机",
                text: "全球金融市场动荡导致经济衰退开始影响我国。出口下降，失业率上升。",
                image: "https://example.com/crisis.jpg",
                choices: [
                    {
                        text: "实施经济刺激计划",
                        effects: {
                            treasury: -8,
                            gdpGrowth: 1.5,
                            approval: 3
                        }
                    },
                    {
                        text: "坚持财政紧缩政策",
                        effects: {
                            gdpGrowth: -1,
                            approval: -10,
                            treasury: 3
                        }
                    }
                ]
            }
        ];

        // 初始化游戏
        function init() {
            // 标签切换
            document.querySelectorAll('.tab').forEach(tab => {
                tab.addEventListener('click', function() {
                    document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
                    this.classList.add('active');
                    
                    const tabId = this.dataset.tab + 'Tab';
                    document.querySelectorAll('.tabContent').forEach(content => {
                        content.classList.remove('active');
                    });
                    document.getElementById(tabId).classList.add('active');
                });
            });

            // 时间控制
            document.querySelectorAll('.timeBtn').forEach((btn, index) => {
                btn.addEventListener('click', function() {
                    document.querySelectorAll('.timeBtn').forEach(b => b.classList.remove('active'));
                    this.classList.add('active');
                    setTimeSpeed(index);
                });
            });

            // 政策按钮
            document.querySelectorAll('.policyActions .btn-primary').forEach(btn => {
                btn.addEventListener('click', function() {
                    const policyName = this.closest('.policyCard').querySelector('.policyName').textContent;
                    implementPolicy(policyName);
                });
            });

            // 科技按钮
            document.querySelectorAll('.techBtn.research').forEach(btn => {
                btn.addEventListener('click', function() {
                    const techName = this.closest('.techCard').querySelector('.techName').textContent;
                    startResearch(techName);
                });
            });

            // 事件选择
            document.querySelectorAll('.choiceBtn').forEach(btn => {
                btn.addEventListener('click', function() {
                    closeEventModal();
                });
            });

            // 开始游戏循环
            updateDisplay();
            setInterval(gameLoop, 1000);
        }

        // 游戏主循环
        function gameLoop() {
            if (gameState.timeSpeed === 0) return;

            // 更新时间
            const monthsToAdd = gameState.timeSpeed;
            gameState.date = new Date(gameState.date.setMonth(gameState.date.getMonth() + monthsToAdd));
            
            // 更新统计数据
            updateStats();
            
            // 随机事件
            if (gameState.eventCooldown <= 0 && Math.random() < 0.1) {
                triggerRandomEvent();
                gameState.eventCooldown = 12; // 1年冷却
            } else {
                gameState.eventCooldown -= monthsToAdd;
            }
            
            updateDisplay();
        }

        // 更新统计数据
        function updateStats() {
            // GDP增长
            gameState.stats.gdp *= (1 + gameState.stats.gdpGrowth / 100);
            
            // 人口增长
            gameState.stats.population *= (1 + gameState.stats.populationGrowth / 100);
            
            // 支持率自然衰减
            gameState.stats.approval -= 0.2;
            
            // 确保数值在合理范围内
            gameState.stats.approval = Math.max(0, Math.min(100, gameState.stats.approval));
            gameState.stats.treasury = Math.max(0, gameState.stats.treasury);
        }

        // 实施政策
        function implementPolicy(policyName) {
            let policyData;
            
            // 在所有分类中查找政策
            for (const category in policies) {
                policyData = policies[category].find(p => p.name === policyName);
                if (policyData) break;
            }
            
            if (!policyData) return;
            
            // 检查是否有足够资金
            if (gameState.stats.treasury < policyData.cost) {
                alert("国库资金不足！");
                return;
            }
            
            // 应用效果
            if (policyData.effects.treasury) gameState.stats.treasury += policyData.effects.treasury;
            if (policyData.effects.gdpGrowth) gameState.stats.gdpGrowth += policyData.effects.gdpGrowth;
            if (policyData.effects.approval) gameState.stats.approval += policyData.effects.approval;
            
            // 添加到已实施政策
            gameState.policies.push({
                name: policyData.name,
                implemented: gameState.date
            });
            
            updateDisplay();
        }

        // 开始研究科技
        function startResearch(techName) {
            const techData = technologies.find(t => t.name === techName);
            if (!techData) return;
            
            // 检查先决条件
            if (techData.requirements.techLevel > gameState.stats.techLevel) {
                alert("科技水平不足，无法研究此技术！");
                return;
            }
            
            // 添加到研究队列
            gameState.technologies.push({
                name: techName,
                started: gameState.date,
                duration: techData.researchTime,
                completed: false
            });
            
            updateDisplay();
        }

        // 触发随机事件
        function triggerRandomEvent() {
            const event = events[Math.floor(Math.random() * events.length)];
            showEventModal(event);
        }

        // 显示事件模态框
        function showEventModal(event) {
            document.getElementById('eventModal').classList.add('active');
            document.querySelector('.modalTitle').textContent = event.title;
            document.querySelector('.modalText').textContent = event.text;
            document.querySelector('.modalImage').style.backgroundImage = `url(${event.image})`;
            
            const choicesContainer = document.querySelector('.modalChoices');
            choicesContainer.innerHTML = '';
            
            event.choices.forEach((choice, index) => {
                const button = document.createElement('button');
                button.className = 'choiceBtn';
                button.textContent = choice.text;
                button.addEventListener('click', () => {
                    // 应用选择的效果
                    if (choice.effects.treasury) gameState.stats.treasury += choice.effects.treasury;
                    if (choice.effects.gdpGrowth) gameState.stats.gdpGrowth += choice.effects.gdpGrowth;
                    if (choice.effects.approval) gameState.stats.approval += choice.effects.approval;
                    
                    closeEventModal();
                    updateDisplay();
                });
                choicesContainer.appendChild(button);
            });
        }

        // 关闭事件模态框
        function closeEventModal() {
            document.getElementById('eventModal').classList.remove('active');
        }

        // 设置游戏速度
        function setTimeSpeed(speed) {
            gameState.timeSpeed = speed;
        }

        // 更新显示
        function updateDisplay() {
            // 更新日期
            const options = { year: 'numeric', month: 'long' };
            document.getElementById('currentDate').textContent = gameState.date.toLocaleDateString('zh-CN', options);
            
            // 更新统计数据
            document.querySelector('.meterFill.gdp').style.width = `${gameState.stats.gdp / 20}%`;
            document.querySelector('.meterFill.approval').style.width = `${gameState.stats.approval}%`;
            document.querySelector('.meterFill.treasury').style.width = `${gameState.stats.treasury}%`;
            document.querySelector('.meterFill.military').style.width = `${gameState.stats.militaryPower}%`;
            
            // 更新数值显示
            document.querySelector('.meterValue:nth-of-type(1)').textContent = `$${(gameState.stats.gdp / 1000).toFixed(2)}万亿`;
            document.querySelector('.meterValue:nth-of-type(2)').textContent = `${Math.round(gameState.stats.approval)}%`;
            document.querySelector('.meterValue:nth-of-type(3)').textContent = `$${gameState.stats.treasury.toFixed(1)}十亿`;
            
            // 更新政策按钮状态
            document.querySelectorAll('.policyActions .btn-primary').forEach(button => {
                const policyName = button.closest('.policyCard').querySelector('.policyName').textContent;
                const alreadyImplemented = gameState.policies.some(p => p.name === policyName);
                button.disabled = alreadyImplemented;
            });
            
            // 更新科技卡状态
            technologies.forEach(tech => {
                const techCard = document.querySelector(`.techCard:has(.techName:contains("${tech.name}"))`);
                if (!techCard) return;
                
                const isResearched = gameState.technologies.some(t => t.name === tech.name && t.completed);
                const isResearching = gameState.technologies.some(t => t.name === tech.name && !t.completed);
                const canResearch = tech.requirements.techLevel <= gameState.stats.techLevel;
                
                techCard.className = 'techCard';
                if (isResearched) {
                    techCard.classList.add('researched');
                } else if (isResearching) {
                    techCard.classList.add('researching');
                } else if (canResearch) {
                    techCard.classList.add('available');
                } else {
                    techCard.classList.add('locked');
                }
                
                const techBtn = techCard.querySelector('.techBtn');
                if (isResearched) {
                    techBtn.className = 'techBtn researched';
                    techBtn.textContent = '已研发';
                } else if (isResearching) {
                    techBtn.className = 'techBtn locked';
                    techBtn.textContent = '研发中...';
                } else if (canResearch) {
                    techBtn.className = 'techBtn research';
                    techBtn.textContent = `研发 (${tech.researchTime/12}年)`;
                } else {
                    techBtn.className = 'techBtn locked';
                    techBtn.textContent = '需要先决条件';
                }
            });
        }

        // 启动游戏
        window.onload = init;
    </script>
</body>
</html>