<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>靜力學平衡方程計算器</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Microsoft JhengHei', '微軟正黑體', sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            color: #333;
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 1000px;
            margin: 0 auto;
            background-color: white;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }
        
        header {
            background: linear-gradient(to right, #2c3e50, #4a6491);
            color: white;
            padding: 25px 30px;
            text-align: center;
        }
        
        h1 {
            font-size: 2.2rem;
            margin-bottom: 10px;
        }
        
        .subtitle {
            font-size: 1.1rem;
            opacity: 0.9;
        }
        
        .main-content {
            display: flex;
            flex-wrap: wrap;
            padding: 20px;
        }
        
        .input-section {
            flex: 1;
            min-width: 300px;
            padding: 20px;
            border-right: 1px solid #eee;
        }
        
        .output-section {
            flex: 1;
            min-width: 300px;
            padding: 20px;
        }
        
        .section-title {
            font-size: 1.4rem;
            color: #2c3e50;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid #4a6491;
        }
        
        .input-group {
            margin-bottom: 25px;
        }
        
        .input-group h3 {
            color: #4a6491;
            margin-bottom: 15px;
            font-size: 1.2rem;
        }
        
        .force-input {
            background-color: #f9f9f9;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 15px;
            border-left: 4px solid #3498db;
        }
        
        .force-input:nth-child(2) {
            border-left-color: #e74c3c;
        }
        
        .force-input:nth-child(3) {
            border-left-color: #2ecc71;
        }
        
        .input-row {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-bottom: 12px;
            align-items: center;
        }
        
        .input-row label {
            min-width: 140px;
            font-weight: 500;
        }
        
        input[type="number"] {
            padding: 10px 12px;
            border: 1px solid #ddd;
            border-radius: 5px;
            width: 120px;
            font-size: 1rem;
        }
        
        .button-group {
            display: flex;
            gap: 15px;
            margin-top: 30px;
            flex-wrap: wrap;
        }
        
        button {
            padding: 14px 24px;
            border: none;
            border-radius: 8px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            flex: 1;
            min-width: 140px;
        }
        
        #calculateBtn {
            background-color: #2ecc71;
            color: white;
        }
        
        #calculateBtn:hover {
            background-color: #27ae60;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(46, 204, 113, 0.3);
        }
        
        #resetBtn {
            background-color: #e74c3c;
            color: white;
        }
        
        #resetBtn:hover {
            background-color: #c0392b;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(231, 76, 60, 0.3);
        }
        
        #addForceBtn {
            background-color: #3498db;
            color: white;
        }
        
        #addForceBtn:hover {
            background-color: #2980b9;
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(52, 152, 219, 0.3);
        }
        
        .result-box {
            background-color: #f8f9fa;
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 25px;
            border-left: 5px solid #3498db;
        }
        
        .result-box h3 {
            color: #2c3e50;
            margin-bottom: 15px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .result-box h3 i {
            font-size: 1.3rem;
        }
        
        .equation {
            font-family: 'Courier New', monospace;
            font-size: 1.2rem;
            background-color: white;
            padding: 12px 15px;
            border-radius: 5px;
            margin: 10px 0;
            border: 1px solid #eee;
        }
        
        .result-value {
            font-size: 1.3rem;
            font-weight: bold;
            color: #2c3e50;
            margin-top: 10px;
            padding: 10px;
            background-color: white;
            border-radius: 5px;
            text-align: center;
        }
        
        .balanced {
            color: #27ae60;
        }
        
        .unbalanced {
            color: #e74c3c;
        }
        
        .summary-section {
            margin-top: 30px;
            background-color: #f8f9fa;
            border-radius: 10px;
            padding: 20px;
            border-top: 3px solid #9b59b6;
        }
        
        .summary-section h3 {
            color: #2c3e50;
            margin-bottom: 15px;
        }
        
        .summary-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 15px;
        }
        
        .summary-item {
            background-color: white;
            padding: 15px;
            border-radius: 8px;
            border: 1px solid #eee;
        }
        
        .summary-item h4 {
            color: #4a6491;
            margin-bottom: 10px;
            font-size: 1rem;
        }
        
        .summary-value {
            font-size: 1.2rem;
            font-weight: bold;
            color: #2c3e50;
        }
        
        .explanation {
            margin-top: 30px;
            background-color: #f0f7ff;
            padding: 20px;
            border-radius: 10px;
            border-left: 5px solid #3498db;
        }
        
        .explanation h3 {
            color: #2c3e50;
            margin-bottom: 15px;
        }
        
        .explanation ul {
            padding-left: 20px;
        }
        
        .explanation li {
            margin-bottom: 10px;
            line-height: 1.5;
        }
        
        footer {
            text-align: center;
            padding: 20px;
            color: #7f8c8d;
            font-size: 0.9rem;
            border-top: 1px solid #eee;
            background-color: #f9f9f9;
        }
        
        @media (max-width: 768px) {
            .main-content {
                flex-direction: column;
            }
            
            .input-section {
                border-right: none;
                border-bottom: 1px solid #eee;
            }
            
            .input-row label {
                min-width: 120px;
            }
            
            .summary-grid {
                grid-template-columns: 1fr;
            }
        }
        
        .symbol {
            font-weight: bold;
            color: #2c3e50;
            background-color: #f1f1f1;
            padding: 2px 6px;
            border-radius: 3px;
            font-family: 'Courier New', monospace;
        }
        
        .force-number {
            display: inline-block;
            width: 24px;
            height: 24px;
            background-color: #4a6491;
            color: white;
            border-radius: 50%;
            text-align: center;
            line-height: 24px;
            margin-right: 8px;
            font-weight: bold;
        }
    </style>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fas fa-balance-scale"></i> 靜力學平衡方程計算器</h1>
            <p class="subtitle">ΣFx = 0 | ΣFy = 0 | ΣM = 0 | 純計算分析工具</p>
        </header>
        
        <div class="main-content">
            <div class="input-section">
                <h2 class="section-title"><i class="fas fa-edit"></i> 輸入外力與力矩</h2>
                
                <div class="input-group">
                    <h3><span class="force-number">1</span> 外力 1 (F₁)</h3>
                    <div class="force-input">
                        <div class="input-row">
                            <label>外力大小 (N):</label>
                            <input type="number" id="f1-magnitude" value="100" step="0.1">
                        </div>
                        <div class="input-row">
                            <label>作用角度 (°):</label>
                            <input type="number" id="f1-angle" value="30" step="0.1">
                        </div>
                        <div class="input-row">
                            <label>作用點 X (m):</label>
                            <input type="number" id="f1-x" value="0" step="0.1">
                        </div>
                        <div class="input-row">
                            <label>作用點 Y (m):</label>
                            <input type="number" id="f1-y" value="0" step="0.1">
                        </div>
                    </div>
                </div>
                
                <div class="input-group">
                    <h3><span class="force-number">2</span> 外力 2 (F₂)</h3>
                    <div class="force-input">
                        <div class="input-row">
                            <label>外力大小 (N):</label>
                            <input type="number" id="f2-magnitude" value="150" step="0.1">
                        </div>
                        <div class="input-row">
                            <label>作用角度 (°):</label>
                            <input type="number" id="f2-angle" value="150" step="0.1">
                        </div>
                        <div class="input-row">
                            <label>作用點 X (m):</label>
                            <input type="number" id="f2-x" value="2" step="0.1">
                        </div>
                        <div class="input-row">
                            <label>作用點 Y (m):</label>
                            <input type="number" id="f2-y" value="0" step="0.1">
                        </div>
                    </div>
                </div>
                
                <div class="input-group">
                    <h3><span class="force-number">3</span> 外力 3 (F₃)</h3>
                    <div class="force-input">
                        <div class="input-row">
                            <label>外力大小 (N):</label>
                            <input type="number" id="f3-magnitude" value="80" step="0.1">
                        </div>
                        <div class="input-row">
                            <label>作用角度 (°):</label>
                            <input type="number" id="f3-angle" value="270" step="0.1">
                        </div>
                        <div class="input-row">
                            <label>作用點 X (m):</label>
                            <input type="number" id="f3-x" value="1" step="0.1">
                        </div>
                        <div class="input-row">
                            <label>作用點 Y (m):</label>
                            <input type="number" id="f3-y" value="1.5" step="0.1">
                        </div>
                    </div>
                </div>
                
                <div class="button-group">
                    <button id="calculateBtn"><i class="fas fa-calculator"></i> 計算平衡狀態</button>
                    <button id="addForceBtn"><i class="fas fa-plus"></i> 新增外力</button>
                    <button id="resetBtn"><i class="fas fa-redo"></i> 重設所有</button>
                </div>
                
                <div class="explanation">
                    <h3><i class="fas fa-info-circle"></i> 使用說明</h3>
                    <ul>
                        <li>輸入外力大小（牛頓 N）、作用角度（度 °）和作用點座標（公尺 m）。</li>
                        <li>角度測量：從正X軸逆時針方向為正。</li>
                        <li>力矩計算以座標原點 (0,0) 為參考點。</li>
                        <li>點擊「計算平衡狀態」進行分析計算。</li>
                        <li>系統平衡條件：ΣFx=0, ΣFy=0, ΣM=0（容許誤差±0.01）。</li>
                    </ul>
                </div>
            </div>
            
            <div class="output-section">
                <h2 class="section-title"><i class="fas fa-chart-bar"></i> 計算結果</h2>
                
                <div class="result-box">
                    <h3><i class="fas fa-arrows-alt-h"></i> X方向力平衡 (ΣFx = 0)</h3>
                    <div class="equation" id="equation-fx">ΣFx = F₁x + F₂x + F₃x + ... = 0</div>
                    <div class="result-value" id="result-fx">等待計算...</div>
                </div>
                
                <div class="result-box">
                    <h3><i class="fas fa-arrows-alt-v"></i> Y方向力平衡 (ΣFy = 0)</h3>
                    <div class="equation" id="equation-fy">ΣFy = F₁y + F₂y + F₃y + ... = 0</div>
                    <div class="result-value" id="result-fy">等待計算...</div>
                </div>
                
                <div class="result-box">
                    <h3><i class="fas fa-sync-alt"></i> 力矩平衡 (ΣM = 0)</h3>
                    <div class="equation" id="equation-m">ΣM = M₁ + M₂ + M₃ + ... = 0</div>
                    <div class="result-value" id="result-m">等待計算...</div>
                </div>
                
                <div class="result-box">
                    <h3><i class="fas fa-check-circle"></i> 系統平衡狀態</h3>
                    <div class="result-value" id="status-equilibrium">等待計算...</div>
                    <p id="equilibrium-detail" style="margin-top: 10px; font-size: 0.95rem; color: #666;"></p>
                </div>
                
                <div class="summary-section">
                    <h3><i class="fas fa-list-alt"></i> 外力分量摘要</h3>
                    <div class="summary-grid" id="force-summary">
                        <!-- 外力分量摘要將由JavaScript動態生成 -->
                    </div>
                </div>
            </div>
        </div>
        
        <footer>
            <p>靜力學平衡方程計算器 - ΣFx=0, ΣFy=0, ΣM=0 | 純計算分析工具</p>
            <p>© 2023 | 靜力學互動系統專題作業</p>
        </footer>
    </div>

    <script>
        // 全域變數儲存外力資料
        let forces = [
            { id: 1, magnitude: 100, angle: 30, x: 0, y: 0 },
            { id: 2, magnitude: 150, angle: 150, x: 2, y: 0 },
            { id: 3, magnitude: 80, angle: 270, x: 1, y: 1.5 }
        ];
        
        let nextForceId = 4;
        
        // DOM 元素
        const calculateBtn = document.getElementById('calculateBtn');
        const resetBtn = document.getElementById('resetBtn');
        const addForceBtn = document.getElementById('addForceBtn');
        
        // 從 forces 資料更新輸入欄位
        function updateInputsFromForces() {
            forces.forEach(force => {
                document.getElementById(`f${force.id}-magnitude`).value = force.magnitude;
                document.getElementById(`f${force.id}-angle`).value = force.angle;
                document.getElementById(`f${force.id}-x`).value = force.x;
                document.getElementById(`f${force.id}-y`).value = force.y;
            });
        }
        
        // 從輸入欄位更新 forces 資料
        function updateForcesFromInputs() {
            forces.forEach(force => {
                force.magnitude = parseFloat(document.getElementById(`f${force.id}-magnitude`).value) || 0;
                force.angle = parseFloat(document.getElementById(`f${force.id}-angle`).value) || 0;
                force.x = parseFloat(document.getElementById(`f${force.id}-x`).value) || 0;
                force.y = parseFloat(document.getElementById(`f${force.id}-y`).value) || 0;
            });
        }
        
        // 計算外力分量
        function calculateForceComponents(magnitude, angle) {
            // 角度轉換：度 → 弧度
            const angleRad = angle * Math.PI / 180;
            
            // 計算 X 和 Y 分量
            const fx = magnitude * Math.cos(angleRad);
            const fy = magnitude * Math.sin(angleRad);
            
            return { fx, fy };
        }
        
        // 計算力矩
        function calculateMoment(force, referenceX = 0, referenceY = 0) {
            const components = calculateForceComponents(force.magnitude, force.angle);
            
            // 相對於參考點的位置向量
            const rx = force.x - referenceX;
            const ry = force.y - referenceY;
            
            // 力矩 = r × F = (rx * Fy) - (ry * Fx)
            // 正值表示逆時針方向力矩
            const moment = (rx * components.fy) - (ry * components.fx);
            
            return moment;
        }
        
        // 計算平衡狀態
        function calculateEquilibrium() {
            updateForcesFromInputs();
            
            let sumFx = 0;
            let sumFy = 0;
            let sumM = 0;
            
            // 方程式字串
            let equationFx = "ΣFx = ";
            let equationFy = "ΣFy = ";
            let equationM = "ΣM = ";
            
            forces.forEach((force, index) => {
                const components = calculateForceComponents(force.magnitude, force.angle);
                const moment = calculateMoment(force);
                
                sumFx += components.fx;
                sumFy += components.fy;
                sumM += moment;
                
                // 建立方程式
                const fxSign = components.fx >= 0 ? "+" : "";
                const fySign = components.fy >= 0 ? "+" : "";
                const mSign = moment >= 0 ? "+" : "";
                
                equationFx += `${index === 0 ? "" : fxSign}${components.fx.toFixed(2)} `;
                equationFy += `${index === 0 ? "" : fySign}${components.fy.toFixed(2)} `;
                equationM += `${index === 0 ? "" : mSign}${moment.toFixed(2)} `;
            });
            
            equationFx += `= <span class="symbol">${sumFx.toFixed(2)}</span>`;
            equationFy += `= <span class="symbol">${sumFy.toFixed(2)}</span>`;
            equationM += `= <span class="symbol">${sumM.toFixed(2)}</span>`;
            
            // 顯示結果
            document.getElementById('equation-fx').innerHTML = equationFx;
            document.getElementById('equation-fy').innerHTML = equationFy;
            document.getElementById('equation-m').innerHTML = equationM;
            
            // 顯示計算值
            const resultFxElement = document.getElementById('result-fx');
            resultFxElement.textContent = `ΣFx = ${sumFx.toFixed(2)} N`;
            resultFxElement.className = `result-value ${Math.abs(sumFx) < 0.01 ? 'balanced' : 'unbalanced'}`;
            
            const resultFyElement = document.getElementById('result-fy');
            resultFyElement.textContent = `ΣFy = ${sumFy.toFixed(2)} N`;
            resultFyElement.className = `result-value ${Math.abs(sumFy) < 0.01 ? 'balanced' : 'unbalanced'}`;
            
            const resultMElement = document.getElementById('result-m');
            resultMElement.textContent = `ΣM = ${sumM.toFixed(2)} N·m`;
            resultMElement.className = `result-value ${Math.abs(sumM) < 0.01 ? 'balanced' : 'unbalanced'}`;
            
            // 判斷系統平衡狀態
            const isEquilibrium = Math.abs(sumFx) < 0.01 && Math.abs(sumFy) < 0.01 && Math.abs(sumM) < 0.01;
            const statusElement = document.getElementById('status-equilibrium');
            const detailElement = document.getElementById('equilibrium-detail');
            
            if (isEquilibrium) {
                statusElement.textContent = "系統處於平衡狀態 (ΣFx=0, ΣFy=0, ΣM=0)";
                statusElement.className = "result-value balanced";
                detailElement.textContent = "所有平衡方程式均滿足，系統處於靜力平衡狀態。";
            } else {
                statusElement.textContent = "系統未達平衡狀態";
                statusElement.className = "result-value unbalanced";
                
                let issues = [];
                if (Math.abs(sumFx) >= 0.01) issues.push(`ΣFx = ${sumFx.toFixed(2)} N ≠ 0`);
                if (Math.abs(sumFy) >= 0.01) issues.push(`ΣFy = ${sumFy.toFixed(2)} N ≠ 0`);
                if (Math.abs(sumM) >= 0.01) issues.push(`ΣM = ${sumM.toFixed(2)} N·m ≠ 0`);
                
                detailElement.textContent = `系統未平衡原因：${issues.join('，')}。`;
            }
            
            // 更新外力分量摘要
            updateForceSummary();
        }
        
        // 更新外力分量摘要
        function updateForceSummary() {
            const summaryContainer = document.getElementById('force-summary');
            summaryContainer.innerHTML = '';
            
            forces.forEach(force => {
                const components = calculateForceComponents(force.magnitude, force.angle);
                const moment = calculateMoment(force);
                
                const summaryItem = document.createElement('div');
                summaryItem.className = 'summary-item';
                summaryItem.innerHTML = `
                    <h4><span class="force-number">${force.id}</span> 外力 ${force.id} (F${force.id})</h4>
                    <div class="summary-value">大小: ${force.magnitude} N</div>
                    <div class="summary-value">角度: ${force.angle}°</div>
                    <div class="summary-value">位置: (${force.x}, ${force.y})</div>
                    <div class="summary-value">Fx: ${components.fx.toFixed(2)} N</div>
                    <div class="summary-value">Fy: ${components.fy.toFixed(2)} N</div>
                    <div class="summary-value">力矩: ${moment.toFixed(2)} N·m</div>
                `;
                
                summaryContainer.appendChild(summaryItem);
            });
        }
        
        // 新增外力
        function addNewForce() {
            const newForce = {
                id: nextForceId,
                magnitude: 50,
                angle: 0,
                x: 0,
                y: 0
            };
            
            forces.push(newForce);
            
            // 建立新外力的輸入區域
            const inputGroup = document.createElement('div');
            inputGroup.className = 'input-group';
            inputGroup.innerHTML = `
                <h3><span class="force-number">${newForce.id}</span> 外力 ${newForce.id} (F${newForce.id})</h3>
                <div class="force-input">
                    <div class="input-row">
                        <label>外力大小 (N):</label>
                        <input type="number" id="f${newForce.id}-magnitude" value="50" step="0.1">
                    </div>
                    <div class="input-row">
                        <label>作用角度 (°):</label>
                        <input type="number" id="f${newForce.id}-angle" value="0" step="0.1">
                    </div>
                    <div class="input-row">
                        <label>作用點 X (m):</label>
                        <input type="number" id="f${newForce.id}-x" value="0" step="0.1">
                    </div>
                    <div class="input-row">
                        <label>作用點 Y (m):</label>
                        <input type="number" id="f${newForce.id}-y" value="0" step="0.1">
                    </div>
                </div>
            `;
            
            // 插入到按鈕之前
            const inputSection = document.querySelector('.input-section');
            const buttonGroup = document.querySelector('.button-group');
            inputSection.insertBefore(inputGroup, buttonGroup);
            
            nextForceId++;
            
            // 重新計算以顯示新外力
            calculateEquilibrium();
        }
        
        // 重設所有輸入
        function resetAll() {
            forces = [
                { id: 1, magnitude: 100, angle: 30, x: 0, y: 0 },
                { id: 2, magnitude: 150, angle: 150, x: 2, y: 0 },
                { id: 3, magnitude: 80, angle: 270, x: 1, y: 1.5 }
            ];
            nextForceId = 4;
            
            // 移除所有額外的輸入區域
            const inputGroups = document.querySelectorAll('.input-group');
            inputGroups.forEach((group, index) => {
                if (index >= 3) {
                    group.remove();
                }
            });
            
            updateInputsFromForces();
            calculateEquilibrium();
        }
        
        // 事件監聽器
        calculateBtn.addEventListener('click', calculateEquilibrium);
        resetBtn.addEventListener('click', resetAll);
        addForceBtn.addEventListener('click', addNewForce);
        
        // 頁面載入時進行計算
        document.addEventListener('DOMContentLoaded', function() {
            calculateEquilibrium();
        });
        
        // 輸入變更時的事件監聽器
        document.addEventListener('input', function(e) {
            if (e.target.type === 'number') {
                // 延遲計算以提升效能
                clearTimeout(window.inputTimeout);
                window.inputTimeout = setTimeout(calculateEquilibrium, 300);
            }
        });
    </script>
</body>
</html>
