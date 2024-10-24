# TimeLineLevTolstoi<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Жизненный путь Льва Толстого</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/tailwindcss/2.2.19/tailwind.min.js"></script>
    <style>
        .timeline-line {
            position: absolute;
            left: 50%;
            transform: translateX(-50%);
            width: 2px;
            height: 100%;
            background: linear-gradient(to bottom, #BFDBFE, #60A5FA, #BFDBFE);
        }
        
        .timeline-event {
            opacity: 0;
            transform: translateY(20px);
            animation: fadeIn 0.5s ease forwards;
        }
        
        @keyframes fadeIn {
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .event-card {
            transition: all 0.3s ease;
        }
        
        .event-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
        }
    </style>
</head>
<body class="bg-gray-50">
    <div class="max-w-5xl mx-auto p-6">
        <h1 class="text-4xl font-bold text-center mb-4 text-blue-900">Жизненный путь Льва Толстого</h1>
        <p class="text-center text-gray-600 mb-8">Интерактивная хронология жизни великого писателя</p>
        
        <div class="relative">
            <div class="timeline-line"></div>
            <div id="timeline-container"></div>
        </div>
    </div>

    <script>
        const events = [
            {
                year: 1828,
                title: "Рождение в Ясной Поляне",
                description: "Лев Николаевич Толстой родился 9 сентября в усадьбе Ясная Поляна",
                details: [
                    "Был четвертым ребенком в семье графа Николая Ильича",
                    "Усадьба Ясная Поляна являлась родовым имением",
                    "При рождении получил титул графа"
                ]
            },
            // Добавьте остальные события здесь
        ];

        function createTimelineEvent(event, index) {
            const isRight = index % 2 === 1;
            const html = `
                <div class="timeline-event flex w-full ${isRight ? 'justify-end' : ''} mb-12">
                    <div class="w-5/12 relative ${isRight ? 'order-1 pl-4' : 'pr-4'}">
                        <div class="event-card bg-white p-4 rounded-lg shadow-lg">
                            <div class="font-bold text-lg text-blue-800">${event.year}</div>
                            <div class="font-semibold text-lg mb-2">${event.title}</div>
                            <p class="text-gray-600">${event.description}</p>
                            <div class="mt-4 hidden details">
                                ${event.details.map(detail => `<p class="text-sm text-gray-700 mt-2">• ${detail}</p>`).join('')}
                            </div>
                            <button class="mt-4 text-blue-500 hover:text-blue-700 text-sm toggle-details">
                                Подробнее...
                            </button>
                        </div>
                        <div class="absolute top-1/2 ${isRight ? '-left-3' : '-right-3'} w-6 h-6 rounded-full bg-blue-500 transform -translate-y-1/2">
                            <div class="absolute inset-0.5 rounded-full bg-white"></div>
                            <div class="absolute inset-1 rounded-full bg-blue-500"></div>
                        </div>
                    </div>
                </div>
            `;
            return html;
        }

        const container = document.getElementById('timeline-container');
        events.forEach((event, index) => {
            container.innerHTML += createTimelineEvent(event, index);
        });

        document.querySelectorAll('.toggle-details').forEach(button => {
            button.addEventListener('click', () => {
                const details = button.previousElementSibling;
                details.classList.toggle('hidden');
                button.textContent = details.classList.contains('hidden') ? 'Подробнее...' : 'Свернуть';
            });
        });
    </script>
</body>
</html>
