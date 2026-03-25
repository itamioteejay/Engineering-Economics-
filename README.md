
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Flourish's 300L Engineering Quiz</title>
    <style>
        :root {
            --primary-color: #2563eb;
            --bg-color: #f8fafc;
            --card-bg: #ffffff;
            --text-color: #1e293b;
        }
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: var(--bg-color);
            color: var(--text-color);
            line-height: 1.6;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
        }
        header {
            text-align: center;
            margin-bottom: 40px;
            padding: 20px;
            background: var(--primary-color);
            color: white;
            border-radius: 12px;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        .question-card {
            background: var(--card-bg);
            padding: 25px;
            margin-bottom: 20px;
            border-radius: 12px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.05);
            border-left: 5px solid var(--primary-color);
        }
        .source-badge {
            display: inline-block;
            background: #e2e8f0;
            color: #475569;
            padding: 4px 8px;
            border-radius: 4px;
            font-size: 0.8rem;
            margin-bottom: 15px;
            font-weight: 600;
        }
        .question-text {
            font-size: 1.1rem;
            font-weight: 600;
            margin-bottom: 15px;
        }
        .options {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }
        .option-label {
            display: flex;
            align-items: center;
            padding: 12px;
            background: #f1f5f9;
            border-radius: 8px;
            cursor: pointer;
            transition: background 0.2s;
        }
        .option-label:hover {
            background: #e2e8f0;
        }
        input[type="radio"] {
            margin-right: 15px;
            transform: scale(1.2);
        }
        button {
            display: block;
            width: 100%;
            padding: 15px;
            font-size: 1.2rem;
            font-weight: bold;
            color: white;
            background: var(--primary-color);
            border: none;
            border-radius: 8px;
            cursor: pointer;
            margin-top: 30px;
            transition: background 0.3s;
        }
        button:hover {
            background: #1d4ed8;
        }
        #results {
            display: none;
            text-align: center;
            margin-top: 30px;
            padding: 20px;
            background: #dcfce7;
            color: #166534;
            border-radius: 8px;
            font-size: 1.5rem;
            font-weight: bold;
        }
        .correct { background: #dcfce7 !important; border: 2px solid #22c55e; }
        .incorrect { background: #fee2e2 !important; border: 2px solid #ef4444; }
    </style>
</head>
<body>

<div class="container">
    <header>
        <h1>Flourish's 300L Mechatronics & Economics Quiz</h1>
        <p>MEE312 & GET311 Interactive Practice</p>
    </header>

    <div id="quiz-container"></div>

    <button onclick="submitQuiz()">Submit Answers & Get Score</button>
    <div id="results"></div>
</div>

<script>
const quizData = [
    // --- ENGINEERING ECONOMICS (Math converted to Multiple Choice) ---
    {
        source: "Topic 1: Simple Interest",
        question: "Find the simple interest on N50,000 for 4 years at 5% per annum.",
        options: ["N5,000", "N10,000", "N15,000", "N20,000"],
        answer: 1
    },
    {
        source: "Topic 1: Simple Interest",
        question: "Calculate the total amount to be repaid on a loan of N20,000 at 10% for 3 years.",
        options: ["N22,000", "N24,000", "N26,000", "N28,000"],
        answer: 2
    },
    {
        source: "Topic 1: Simple Interest",
        question: "A man invests N150,000 and earns N45,000 in interest over 3 years. What is the interest rate?",
        options: ["5%", "8%", "10%", "12%"],
        answer: 2
    },
    {
        source: "Topic 1: Simple Interest",
        question: "How long will it take for N10,000 to double itself at 10% simple interest?",
        options: ["5 years", "8 years", "10 years", "12 years"],
        answer: 2
    },
    {
        source: "Topic 1: Simple Interest",
        question: "Find the principal if the interest is N2,500, rate is 5%, and time is 2 years.",
        options: ["N20,000", "N25,000", "N30,000", "N35,000"],
        answer: 1
    },
    {
        source: "Topic 1: Simple Interest",
        question: "Calculate the interest on N75,000 for 6 months at 20% per annum.",
        options: ["N5,000", "N6,500", "N7,500", "N8,500"],
        answer: 2
    },
    {
        source: "Topic 1: Simple Interest",
        question: "A student earned N500 interest on a N5,000 deposit. If the time was 2 years, find the rate.",
        options: ["3%", "5%", "7%", "10%"],
        answer: 1
    },
    {
        source: "Topic 1: Simple Interest",
        question: "What is the amount on N120,000 for 5 years at 12.5% simple interest?",
        options: ["N175,000", "N185,000", "N195,000", "N205,000"],
        answer: 2
    },
    {
        source: "Topic 1: Simple Interest",
        question: "If a bank offers 15% interest, how much interest does N1,000,000 earn in 3 months?",
        options: ["N25,000", "N30,000", "N37,500", "N45,000"],
        answer: 2
    },
    {
        source: "Topic 1: Simple Interest",
        question: "Find the time required for N80,000 to yield N12,000 interest at 3% per annum.",
        options: ["3 years", "4 years", "5 years", "6 years"],
        answer: 2
    },
    {
        source: "Topic 2: Compound Interest",
        question: "Find the compound amount of N10,000 for 2 years at 10%.",
        options: ["N11,000", "N12,000", "N12,100", "N13,000"],
        answer: 2
    },
    {
        source: "Topic 2: Compound Interest",
        question: "Calculate the amount on N5,000 for 3 years at 5%.",
        options: ["N5,500", "N5,788", "N6,000", "N6,250"],
        answer: 1
    },
    {
        source: "Topic 2: Compound Interest",
        question: "N20,000 is invested at 20% compounded annually for 2 years. Find the interest only.",
        options: ["N4,000", "N8,000", "N8,800", "N9,600"],
        answer: 2
    },
    {
        source: "Topic 2: Compound Interest",
        question: "Find the future value of N50,000 compounded semi-annually for 1 year at 10%.",
        options: ["N55,000", "N55,125", "N55,250", "N56,000"],
        answer: 1
    },
    {
        source: "Topic 2: Compound Interest",
        question: "Calculate the amount for N100,000 at 8% compounded quarterly for 1 year.",
        options: ["N108,000", "N108,243", "N108,500", "N109,000"],
        answer: 1
    },

    // --- FUTM-GET311 ROSHTECH ---
    {
        source: "FUTM-GET311",
        question: "Rational decision-making process involves the following procedural steps?",
        options: ["Identifying objectives and defining the problem", "Ignoring alternatives to save time", "Decision based on intuition only", "Skipping the evaluation of results"],
        answer: 0
    },
    {
        source: "FUTM-GET311",
        question: "What is defined as the interest on a loan or principal?",
        options: ["Capital gain", "Simple interest", "Cost of money", "Salvage value"],
        answer: 1
    },
    {
        source: "FUTM-GET311",
        question: "What is based only on the original amount of the loan or principal?",
        options: ["Compound interest", "Simple interest", "Effective interest", "Nominal interest"],
        answer: 1
    },
    {
        source: "FUTM-GET311",
        question: "What is defined as any tangible economic product that contributes directly or indirectly to the satisfaction of human want?",
        options: ["Services", "Goods", "Capital", "Labor"],
        answer: 1
    },
    {
        source: "FUTM-GET311",
        question: "What refers to the account of money value for the uses of borrowed capital?",
        options: ["Interest", "Principal", "Asset", "Liability"],
        answer: 0
    },
    {
        source: "FUTM-GET311",
        question: "What is the type of annuity where the first payment does not begin until some late date in the cash flow?",
        options: ["Ordinary annuity", "Annuity due", "Deferred annuity", "Perpetuity"],
        answer: 2
    },
    {
        source: "FUTM-GET311",
        question: "All are classified under direct labour expenses except one?",
        options: ["Basic wages", "Overtime premiums", "Production bonuses", "Administrative salaries"],
        answer: 3
    },
    {
        source: "FUTM-GET311",
        question: "At a level of production, sales volumes, or sales value where the organization neither makes a profit nor a loss is known as:",
        options: ["Profit margin", "Break-even point", "Equilibrium", "Sunk cost"],
        answer: 1
    },
    {
        source: "FUTM-GET311",
        question: "What refers to the cost of borrowing money or the amount earned by a unit principal per unit time?",
        options: ["Interest rate", "Discount rate", "Inflation rate", "Yield rate"],
        answer: 0
    },
    {
        source: "FUTM-GET311",
        question: "Which of the following defines the meaning of engineering economics?",
        options: ["Study of pure economic theories", "Application of economic techniques to engineering projects", "Historical study of engineering", "Management of human resources only"],
        answer: 1
    },
    {
        source: "FUTM-GET311",
        question: "What refers to the cost of loss in terms of investment evaluation?",
        options: ["Fixed cost", "Opportunity cost", "Marginal cost", "Variable cost"],
        answer: 1
    },
    {
        source: "FUTM-GET311",
        question: "The implication of salvage value is:",
        options: ["The initial cost of an asset", "The value of an asset at the end of its useful life", "The annual maintenance cost", "The tax paid on an asset"],
        answer: 1
    },
    {
        source: "FUTM-GET311",
        question: "Which of the following taxes do we apply even analysis (Break-even analysis)?",
        options: ["Luxury tax", "Income tax", "Indirect tax", "Property tax"],
        answer: 1
    },
    {
        source: "FUTM-GET311",
        question: "Different sums of money possessing equal value over an interest period are said to be:",
        options: ["Equal", "Equivalent", "Proportionate", "Balanced"],
        answer: 1
    },
    {
        source: "FUTM-GET311",
        question: "The following constitute variable cost in a manufacturing setup except:",
        options: ["Raw materials", "Direct labour", "Rent of the factory building", "Electricity for production"],
        answer: 2
    },

    // --- MEE312 ---
    {
        source: "MEE312",
        question: "What is defined as an entity which makes product, good or services available to buyer or consumer in exchange of monetary consideration?",
        options: ["Seller", "Manufacturer", "Producer", "Buyer or consumer"],
        answer: 0
    },
    {
        source: "MEE312",
        question: "What is considered as the basic consuming or demanding unit of a commodity?",
        options: ["Seller", "Manufacturer", "Producer", "Buyer or consumer"],
        answer: 3
    },
    {
        source: "MEE312",
        question: "What refers to the goods and services that are desired by human and will be acquired only after all the needs have been satisfied?",
        options: ["Producer products", "Consumer products", "Luxury", "Necessity"],
        answer: 2
    },
    {
        source: "MEE312",
        question: "What refers to the goods and services that are required to support human life, needs and activities?",
        options: ["Producer products", "Consumer products", "Luxury", "Necessity"],
        answer: 3
    },
    {
        source: "MEE312",
        question: "What is defined as any tangible economic activity that contributes directly or indirectly to the satisfaction of human want?",
        options: ["Services", "Goods", "Commodities", "Goods or commodities"],
        answer: 1
    },
    {
        source: "MEE312",
        question: "What is defined as any tangible economic product that contributes directly or indirectly to the satisfaction of human want?",
        options: ["Services", "Goods", "Commodities", "Goods or commodities"],
        answer: 1
    },
    {
        source: "MEE312",
        question: "What is defines as the analysis and evaluation of the monetary consequences by using the theories and principles of economics to engineering applications, designs and projects?",
        options: ["Economic Analysis", "Engineering cost analysis", "Engineering economy", "Design cost analysis"],
        answer: 2
    },
    {
        source: "MEE312",
        question: "The Saudi Arabian Oil Refinery developed an oil well which is estimated to contain 5,000,000 barrels of oil at an initial cost of $ 50,000,000. What is the depletion charge during the year where it produces half million barrels of oil?",
        options: ["$ 5,000,000.00", "$ 5,010,000.00", "$ 5,025,000.00", "$ 5,050,000.00"],
        answer: 0
    },
    {
        source: "MEE312",
        question: "An asset is purchased for P 9,000.00. Its estimated economic life is 10 years after which it will be sold for P 1,000.00. Find the depreciation in the first three years using sum-of-years digit method",
        options: ["P 3,279.27", "P 3,927.27", "P 3,729.27", "P 3,792.72"],
        answer: 1
    },
    {
        source: "MEE312",
        question: "A man loans P 187,400 from a bank with interest at 5% compounded annually. He agrees to pay his obligations by paying 8 equal annual payments, the first being due at the end of 10 years. Find the annual payments.",
        options: ["P 43,600.10", "P 43,489.47", "P 43,263.91", "P 43,763.20"],
        answer: 1
    },
    {
        source: "MEE312",
        question: "What is the present worth of a year annuity paying P 3,000.00 at the end of each year, with interest at 8% compounded annually?",
        options: ["P 7,654.04", "P 7,731.29", "P 7,420.89", "P 7,590.12"],
        answer: 1
    },
    {
        source: "MEE312",
        question: "A factory operator bought a diesel generator set for P 10,000.00 and agreed to pay the dealer uniform sum at the end of each year for 5 years at 8% interest compounded annually. What is the annual payment?",
        options: ["P 2,500.57", "P 2,544.45", "P 2,540.56", "P 2,504.57"],
        answer: 3
    },
    {
        source: "MEE312",
        question: "What annuity is required over 12 years to equate with a future amount of P 20,000? Assume i=6% annually.",
        options: ["P 1,290.34", "P 1,185.54", "P 1,107.34", "P 1,205.74"],
        answer: 1
    },
    {
        source: "MEE312",
        question: "What is the present worth of a P500 annuity starting at the end of the third year and continuing to the end of the fourth year, if the annual interest rate is 10%?",
        options: ["P 727.17", "P 717.17", "P 714.71", "P 731.17"],
        answer: 1
    },
    {
        source: "MEE312",
        question: "Two proposals being considered: A. Construction now to cost P 400,000. B. Construction of a smaller building now to cost P300,000 and at the end of 5 years, an extension to be added to cost P 200,000. By how much is proposal B more economical than proposal A if interest rate is 20%?",
        options: ["P 19,122.15", "P 19,423.69", "P 19,518.03", "P 19,624.49"],
        answer: 0
    }
];

const container = document.getElementById('quiz-container');

quizData.forEach((q, index) => {
    const card = document.createElement('div');
    card.className = 'question-card';
    card.id = `card-${index}`;

    const badge = document.createElement('div');
    badge.className = 'source-badge';
    badge.innerText = q.source;

    const questionText = document.createElement('div');
    questionText.className = 'question-text';
    questionText.innerText = `${index + 1}. ${q.question}`;

    const optionsDiv = document.createElement('div');
    optionsDiv.className = 'options';

    q.options.forEach((opt, optIndex) => {
        const label = document.createElement('label');
        label.className = 'option-label';
        label.id = `label-${index}-${optIndex}`;
        
        const input = document.createElement('input');
        input.type = 'radio';
        input.name = `question${index}`;
        input.value = optIndex;

        label.appendChild(input);
        label.appendChild(document.createTextNode(opt));
        optionsDiv.appendChild(label);
    });

    card.appendChild(badge);
    card.appendChild(questionText);
    card.appendChild(optionsDiv);
    container.appendChild(card);
});

function submitQuiz() {
    let score = 0;
    
    quizData.forEach((q, index) => {
        const selected = document.querySelector(`input[name="question${index}"]:checked`);
        const correctLabel = document.getElementById(`label-${index}-${q.answer}`);
        
        // Reset styles
        document.querySelectorAll(`input[name="question${index}"]`).forEach(input => {
            input.parentElement.classList.remove('correct', 'incorrect');
        });

        if (selected) {
            const selectedVal = parseInt(selected.value);
            if (selectedVal === q.answer) {
                score++;
                selected.parentElement.classList.add('correct');
            } else {
                selected.parentElement.classList.add('incorrect');
                correctLabel.classList.add('correct');
            }
        } else {
            correctLabel.classList.add('correct');
        }
    });

    const resultsDiv = document.getElementById('results');
    resultsDiv.style.display = 'block';
    resultsDiv.innerText = `You scored ${score} out of ${quizData.length}!`;
    window.scrollTo({ top: document.body.scrollHeight, behavior: 'smooth' });
}
</script>

</body>
</html>
