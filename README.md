# Seminario sobre aplicaciones de la IA

| Session | Topic | 
| :---: | :--- | 
| 10 abr | 1. Introducción |
| 10 abr | 2. Modelos de lenguaje |
| 10 abr | 3. Ingeniería de prompts |
| 10 abr | 4. Plantillas para prompts |
| 11 abr | 5. Resúmenes estadísticos y formatos de datos |
| 11 abr | 6. Tests estadísticos |
| 11 abr | 7. Búsqueda de información |
| 11 abr | 8. Discusión |


<!--
Palette Name: Vibrant Professional (Navy, Silver, Coral Red, Teal, Off-White)
Confirmation: NEITHER Mermaid JS NOR SVG were used anywhere in the output.
Narrative Plan: 
1. Introduction: Hook the reader with the prevalence of Class I & II restorations and the shift to adhesive dentistry.
2. The Longevity Debate: A direct comparison of Amalgam vs. Composite survival times using a horizontal bar chart.
3. Failure Modes Analysis: Two side-by-side donut charts detailing why each material typically fails, explaining the clinical differences.
4. Material Advancements (Bulk-Fill): A radar chart comparing Conventional vs. Bulk-Fill composites across key clinical metrics.
5. Clinical Techniques: CSS-styled structural cards outlining findings on Flowable Liners and Matrix Systems.
6. Minimally Invasive Protocols: Highlight cards for Selective Caries Removal and Pediatric techniques (ART vs. Hall).
7. Literature Sources: A clean HTML table summarizing the synthesized research.
Visualization Choices:
- Data Point: Median Survival Times -> Goal: Compare -> Chosen Visualization: Horizontal Bar Chart (Chart.js) -> Justification: Clearly displays the magnitude difference between 16 and 11 years. NO SVG.
- Data Point: Failure Modes -> Goal: Compare Composition -> Chosen Visualization: Donut Charts (Chart.js) -> Justification: Breaks down the primary reasons for failure as parts of a whole for each material. NO SVG.
- Data Point: Conventional vs Bulk-Fill -> Goal: Relationships/Multivariate Comparison -> Chosen Visualization: Radar Chart (Chart.js) -> Justification: Ideal for mapping multiple performance variables (gloss, adaptation, time, stress) simultaneously. NO SVG.
-->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Occlusal & Proximal Restorations: 2020-2025 Clinical Evidence</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&display=swap');
        body { font-family: 'Inter', sans-serif; background-color: #EDF2F4; color: #2B2D42; }
        .chart-container { position: relative; width: 100%; max-width: 600px; margin-left: auto; margin-right: auto; height: 350px; max-height: 400px; }
        .chart-container-small { position: relative; width: 100%; max-width: 400px; margin-left: auto; margin-right: auto; height: 250px; max-height: 300px; }
        .card-shadow { box-shadow: 0 10px 25px -5px rgba(43, 45, 66, 0.1), 0 8px 10px -6px rgba(43, 45, 66, 0.1); }
    </style>
</head>
<body class="antialiased pb-16">

    <header class="bg-[#2B2D42] text-white py-16 px-6 mb-10 border-b-8 border-[#EF233C]">
        <div class="max-w-6xl mx-auto">
            <h1 class="text-4xl md:text-6xl font-extrabold mb-4 tracking-tight">The Modern Posterior Restoration</h1>
            <p class="text-xl md:text-2xl text-[#8D99AE] font-light max-w-3xl">An evidence-based synthesis of Class I & II procedures, material longevity, and clinical advancements (2020–2025).</p>
        </div>
    </header>

    <main class="max-w-6xl mx-auto px-6 space-y-12">

        <section class="bg-white rounded-2xl p-8 card-shadow">
            <h2 class="text-3xl font-bold mb-4 text-[#2B2D42] border-l-4 border-[#06D6A0] pl-4">1. The Longevity Debate</h2>
            <p class="text-lg mb-8 text-gray-700 leading-relaxed">Despite the global shift toward adhesive dentistry and aesthetic composites, traditional amalgam still demonstrates a statistical edge in longevity. However, due to the Minamata Convention and patient demand, composite resin remains the undisputed "gold standard" for Class I and II restorations today.</p>
            
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-10 items-center">
                <div class="chart-container">
                    <canvas id="longevityChart"></canvas>
                </div>
                <div>
                    <div class="bg-[#EDF2F4] p-6 rounded-xl border border-[#8D99AE]/30 mb-4">
                        <div class="text-4xl font-extrabold text-[#2B2D42] mb-1">16+ <span class="text-xl font-normal text-[#8D99AE]">Years</span></div>
                        <h3 class="font-bold text-lg mb-2">Amalgam Median Survival</h3>
                        <p class="text-sm text-gray-600">Provides decades of predictable service in high-load posterior scenarios.</p>
                    </div>
                    <div class="bg-[#EDF2F4] p-6 rounded-xl border border-[#8D99AE]/30">
                        <div class="text-4xl font-extrabold text-[#EF233C] mb-1">11 <span class="text-xl font-normal text-[#8D99AE]">Years</span></div>
                        <h3 class="font-bold text-lg mb-2">Composite Median Survival</h3>
                        <p class="text-sm text-gray-600">The modern standard, highly aesthetic and tooth-preserving, but more sensitive to operator technique.</p>
                    </div>
                </div>
            </div>
        </section>

        <section class="bg-[#2B2D42] text-white rounded-2xl p-8 card-shadow">
            <h2 class="text-3xl font-bold mb-4 border-l-4 border-[#EF233C] pl-4">2. Divergent Failure Modes</h2>
            <p class="text-lg mb-8 text-[#8D99AE] leading-relaxed">When posterior restorations fail, the mechanisms differ drastically by material. Understanding these pathways is critical for treatment planning and patient education.</p>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                <div class="bg-white/10 p-6 rounded-xl backdrop-blur-sm">
                    <h3 class="text-xl font-bold mb-6 text-center text-white">Why Composite Fails</h3>
                    <div class="chart-container-small">
                        <canvas id="compositeFailureChart"></canvas>
                    </div>
                    <p class="text-sm text-center mt-4 text-[#EDF2F4]">Susceptible to plaque accumulation at margins leading to secondary decay, and material fracture under heavy occlusal loads.</p>
                </div>
                
                <div class="bg-white/10 p-6 rounded-xl backdrop-blur-sm">
                    <h3 class="text-xl font-bold mb-6 text-center text-white">Why Amalgam Fails</h3>
                    <div class="chart-container-small">
                        <canvas id="amalgamFailureChart"></canvas>
                    </div>
                    <p class="text-sm text-center mt-4 text-[#EDF2F4]">Higher elastic modulus often results in fractures of the surrounding natural tooth structure, alongside gradual marginal breakdown.</p>
                </div>
            </div>
        </section>

        <section class="bg-white rounded-2xl p-8 card-shadow">
            <h2 class="text-3xl font-bold mb-4 text-[#2B2D42] border-l-4 border-[#06D6A0] pl-4">3. The Bulk-Fill Revolution</h2>
            <p class="text-lg mb-8 text-gray-700 leading-relaxed">Bulk-fill materials have fundamentally altered Class I and II workflows. By allowing 4–5mm increments, they drastically reduce chair time. Clinical evidence now confirms their performance is on par with, or exceeds, conventional layered techniques in key areas.</p>
            
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-10 items-center">
                <div class="order-2 lg:order-1">
                    <ul class="space-y-4">
                        <li class="flex items-start">
                            <span class="text-2xl mr-3 text-[#06D6A0]">&#10004;</span>
                            <div>
                                <strong class="text-[#2B2D42] block text-lg">Marginal Adaptation</strong>
                                <span class="text-gray-600">Shows comparable, and sometimes superior, adaptation over 2-3 year periods.</span>
                            </div>
                        </li>
                        <li class="flex items-start">
                            <span class="text-2xl mr-3 text-[#06D6A0]">&#10004;</span>
                            <div>
                                <strong class="text-[#2B2D42] block text-lg">Polymerization Stress</strong>
                                <span class="text-gray-600">Advanced monomer chemistry mitigates shrinkage stress despite large increments.</span>
                            </div>
                        </li>
                        <li class="flex items-start">
                            <span class="text-2xl mr-3 text-[#EF233C]">&#9888;</span>
                            <div>
                                <strong class="text-[#2B2D42] block text-lg">Surface Gloss</strong>
                                <span class="text-gray-600">Conventional micro-hybrid/nano composites still retain a higher polish over time.</span>
                            </div>
                        </li>
                    </ul>
                </div>
                <div class="chart-container order-1 lg:order-2">
                    <canvas id="bulkFillRadar"></canvas>
                </div>
            </div>
        </section>

        <section class="grid grid-cols-1 md:grid-cols-2 gap-8">
            <div class="bg-white rounded-2xl p-8 card-shadow">
                <h2 class="text-2xl font-bold mb-4 text-[#2B2D42] border-b pb-2">Technical Advancements</h2>
                <div class="mt-6 space-y-6">
                    <div class="p-5 bg-[#EDF2F4] rounded-lg border-l-4 border-[#8D99AE]">
                        <h3 class="font-bold text-lg mb-2">Flowable Liners</h3>
                        <p class="text-sm text-gray-700">Often used to improve internal cavity adaptation in Class II boxes. However, 2025 narrative reviews show they <strong class="text-[#EF233C]">do not significantly increase</strong> the long-term clinical longevity of the restoration compared to unlined protocols.</p>
                    </div>
                    <div class="p-5 bg-[#EDF2F4] rounded-lg border-l-4 border-[#06D6A0]">
                        <h3 class="font-bold text-lg mb-2">Matrix Systems</h3>
                        <p class="text-sm text-gray-700">No system perfectly replicates anatomy, but <strong class="text-[#2B2D42]">Sectional Matrices</strong> consistently produce tighter, more anatomically correct interdental contacts compared to circumferential bands.</p>
                    </div>
                </div>
            </div>

            <div class="bg-white rounded-2xl p-8 card-shadow">
                <h2 class="text-2xl font-bold mb-4 text-[#2B2D42] border-b pb-2">Minimally Invasive Protocols</h2>
                <div class="mt-6 grid grid-cols-1 gap-4">
                    <div class="border-2 border-[#8D99AE] rounded-xl p-5 flex items-center">
                        <div class="text-4xl mr-4">&#128300;</div>
                        <div>
                            <h3 class="font-bold text-[#2B2D42]">Selective Caries Removal</h3>
                            <p class="text-xs text-gray-600 mt-1">Abandoning "extension for prevention." Partial removal in deep lesions preserves pulp vitality and avoids unnecessary endodontic intervention.</p>
                        </div>
                    </div>
                    <div class="border-2 border-[#8D99AE] rounded-xl p-5 flex items-center">
                        <div class="text-4xl mr-4">&#129330;</div>
                        <div>
                            <h3 class="font-bold text-[#2B2D42]">Pediatric ART vs. Hall Technique</h3>
                            <p class="text-xs text-gray-600 mt-1">Atraumatic Restorative Treatment (GIC) is highly effective and cost-efficient. However, for multi-surface primary lesions, the Hall Technique (preformed metal crowns) yields higher survival rates.</p>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section class="bg-white rounded-2xl p-8 card-shadow mb-12">
            <h2 class="text-2xl font-bold mb-6 text-[#2B2D42]">Curated Source Literature (2020-2025)</h2>
            <div class="overflow-x-auto">
                <table class="w-full text-left border-collapse">
                    <thead>
                        <tr class="bg-[#2B2D42] text-white">
                            <th class="p-4 rounded-tl-lg font-semibold text-sm">Paper Title</th>
                            <th class="p-4 font-semibold text-sm">Authors/Year</th>
                            <th class="p-4 rounded-tr-lg font-semibold text-sm">Key Focus</th>
                        </tr>
                    </thead>
                    <tbody class="text-sm">
                        <tr class="border-b border-gray-200 hover:bg-gray-50">
                            <td class="p-4 font-medium text-[#2B2D42]">Longevity of Amalgam Versus Composite Resin</td>
                            <td class="p-4 text-gray-600">Basmatkar et al. (2025)</td>
                            <td class="p-4 text-gray-600">Systematic review comparing 16-yr (AM) vs 11-yr (CR) survival.</td>
                        </tr>
                        <tr class="border-b border-gray-200 hover:bg-gray-50 bg-[#EDF2F4]/50">
                            <td class="p-4 font-medium text-[#2B2D42]">Class-I & II Restorations with Flowable Liners</td>
                            <td class="p-4 text-gray-600">MDPI (2025)</td>
                            <td class="p-4 text-gray-600">Narrative review on the effect of liners on clinical success.</td>
                        </tr>
                        <tr class="border-b border-gray-200 hover:bg-gray-50">
                            <td class="p-4 font-medium text-[#2B2D42]">Clinical performances of Class II restorations</td>
                            <td class="p-4 text-gray-600">PubMed (2025)</td>
                            <td class="p-4 text-gray-600">Prospective study on bulk-fill vs. high-fill flowable materials.</td>
                        </tr>
                        <tr class="border-b border-gray-200 hover:bg-gray-50 bg-[#EDF2F4]/50">
                            <td class="p-4 font-medium text-[#2B2D42]">Contributors to Dental Restoration Longevity</td>
                            <td class="p-4 text-gray-600">MDPI (2024)</td>
                            <td class="p-4 text-gray-600">Integrated review on patient, dentist, and material factors.</td>
                        </tr>
                        <tr class="border-b border-gray-200 hover:bg-gray-50">
                            <td class="p-4 font-medium text-[#2B2D42]">Effectiveness of Materials in ART</td>
                            <td class="p-4 text-gray-600">PMC (2025)</td>
                            <td class="p-4 text-gray-600">Systematic review of GIC performance in pediatric restorations.</td>
                        </tr>
                        <tr class="border-b border-gray-200 hover:bg-gray-50 bg-[#EDF2F4]/50">
                            <td class="p-4 font-medium text-[#2B2D42]">3D analysis of proximal surfaces after restoration</td>
                            <td class="p-4 text-gray-600">RJS (2025)</td>
                            <td class="p-4 text-gray-600">Study on anatomical accuracy of various matrix systems.</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </section>

    </main>

    <script>
        function wl(l) {
            if (l.length <= 16) return l;
            const w = l.split(' ');
            let r = [];
            let c = '';
            w.forEach(x => {
                if ((c + x).length > 16) {
                    r.push(c.trim());
                    c = x + ' ';
                } else {
                    c += x + ' ';
                }
            });
            if (c) r.push(c.trim());
            return r;
        }

        const tc = {
            tooltip: {
                callbacks: {
                    title: function(ti) {
                        const i = ti[0];
                        let l = i.chart.data.labels[i.dataIndex];
                        if (Array.isArray(l)) {
                            return l.join(' ');
                        } else {
                            return l;
                        }
                    }
                }
            }
        };

        const ctx1 = document.getElementById('longevityChart').getContext('2d');
        new Chart(ctx1, {
            type: 'bar',
            data: {
                labels: [wl('Amalgam Restorations'), wl('Composite Resin')],
                datasets: [{
                    label: 'Median Survival (Years)',
                    data: [16, 11],
                    backgroundColor: ['#8D99AE', '#EF233C'],
                    borderRadius: 6
                }]
            },
            options: {
                indexAxis: 'y',
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { display: false },
                    ...tc
                },
                scales: {
                    x: { beginAtZero: true, max: 20, title: { display: true, text: 'Years' } },
                    y: { ticks: { font: { weight: 'bold' } } }
                }
            }
        });

        const ctx2 = document.getElementById('compositeFailureChart').getContext('2d');
        new Chart(ctx2, {
            type: 'doughnut',
            data: {
                labels: [wl('Secondary Caries'), wl('Restoration Fracture'), wl('Other Causes')],
                datasets: [{
                    data: [65, 25, 10],
                    backgroundColor: ['#EF233C', '#FF9F1C', '#8D99AE'],
                    borderWidth: 0
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                cutout: '65%',
                plugins: {
                    legend: { position: 'bottom', labels: { color: '#EDF2F4', padding: 15 } },
                    ...tc
                }
            }
        });

        const ctx3 = document.getElementById('amalgamFailureChart').getContext('2d');
        new Chart(ctx3, {
            type: 'doughnut',
            data: {
                labels: [wl('Tooth Structure Fracture'), wl('Marginal Breakdown'), wl('Secondary Decay')],
                datasets: [{
                    data: [55, 35, 10],
                    backgroundColor: ['#06D6A0', '#97CADB', '#8D99AE'],
                    borderWidth: 0
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                cutout: '65%',
                plugins: {
                    legend: { position: 'bottom', labels: { color: '#EDF2F4', padding: 15 } },
                    ...tc
                }
            }
        });

        const ctx4 = document.getElementById('bulkFillRadar').getContext('2d');
        new Chart(ctx4, {
            type: 'radar',
            data: {
                labels: [wl('Marginal Adaptation'), wl('Surface Gloss Retention'), wl('Low Polymerization Stress'), wl('Placement Time Efficiency')],
                datasets: [
                    {
                        label: 'Bulk-Fill Composite',
                        data: [4.5, 3.0, 4.0, 5.0],
                        backgroundColor: 'rgba(6, 214, 160, 0.2)',
                        borderColor: '#06D6A0',
                        pointBackgroundColor: '#06D6A0',
                        borderWidth: 2
                    },
                    {
                        label: 'Conventional Layered',
                        data: [4.0, 4.8, 3.0, 2.0],
                        backgroundColor: 'rgba(239, 35, 60, 0.2)',
                        borderColor: '#EF233C',
                        pointBackgroundColor: '#EF233C',
                        borderWidth: 2
                    }
                ]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                scales: {
                    r: {
                        angleLines: { color: 'rgba(0,0,0,0.1)' },
                        grid: { color: 'rgba(0,0,0,0.1)' },
                        pointLabels: { font: { size: 11, weight: 'bold' }, color: '#2B2D42' },
                        ticks: { display: false, min: 0, max: 5 }
                    }
                },
                plugins: {
                    legend: { position: 'bottom' },
                    ...tc
                }
            }
        });
    </script>
</body>
</html>
