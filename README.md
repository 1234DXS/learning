<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="Content-Security-Policy" content="upgrade-insecure-requests">
    <title>CodeMaster - 编程语言学习资源大全</title>
    <!-- 先加载CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
<!-- 后加载JS -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js" defer></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css">
    <style>
        :root {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --light-bg: #f8f9fa;
            --dark-bg: #1a1a2e;
            --text-light: #f8f9fa;
            --text-dark: #212529;
            --card-radius: 12px;
            --icon-radius: 8px;
            --transition-speed: 0.25s;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            transition: all var(--transition-speed);
            scroll-behavior: smooth;
        }
        
        .dark-mode {
            background-color: var(--dark-bg);
            color: var(--text-light);
        }
        
        .light-mode {
            background-color: var(--light-bg);
            color: var(--text-dark);
        }
        
        .navbar {
            background-color: var(--primary-color);
            transition: all var(--transition-speed);
        }
        
        .language-card {
            transition: all var(--transition-speed);
            margin-bottom: 20px;
            height: 100%;
            border-radius: var(--card-radius);
            overflow: hidden;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        
        .language-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 12px 24px rgba(0,0,0,0.15);
        }
        
        .language-icon {
            width: 60px;
            height: 60px;
            object-fit: contain;
            border-radius: var(--icon-radius);
            transition: all var(--transition-speed);
        }
        
        .progress-tracker {
            height: 10px;
            border-radius: 5px;
        }
        
        .resource-item {
            padding: 12px;
            border-radius: var(--card-radius);
            margin-bottom: 8px;
            transition: all var(--transition-speed);
        }
        
        .resource-item:hover {
            transform: translateX(5px);
        }
        
        .comparison-table {
            width: 100%;
            overflow-x: auto;
            border-radius: var(--card-radius);
        }
        
        .btn {
            transition: all var(--transition-speed) !important;
            border-radius: var(--card-radius);
        }
        
        .modal-content {
            border-radius: var(--card-radius);
        }
        
        .tab-content {
            border-radius: 0 0 var(--card-radius) var(--card-radius);
        }
        
        .nav-tabs .nav-link {
            border-radius: var(--card-radius) var(--card-radius) 0 0 !important;
        }
        
        .smooth-transition {
            transition: all var(--transition-speed);
        }
        
        @media (max-width: 768px) {
            :root {
                --card-radius: 10px;
            }
            
            .language-card {
                margin-bottom: 15px;
            }
        }
    </style>
</head>
<body class="light-mode">
    <!-- 导航栏 -->
    <nav class="navbar navbar-expand-lg navbar-dark sticky-top">
        <div class="container">
            <a class="navbar-brand" href="#">
                <i class="fas fa-code me-2"></i>CodeMaster
            </a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav me-auto">
                    <li class="nav-item">
                        <a class="nav-link active" href="#home">首页</a>
                    </li>
                    <li class="nav-item dropdown">
                        <a class="nav-link dropdown-toggle" href="#" id="languagesDropdown" role="button" data-bs-toggle="dropdown">
                            编程语言
                        </a>
                        <ul class="dropdown-menu">
                            <li><h6 class="dropdown-header">热门语言</h6></li>
                            <li><a class="dropdown-item" href="#python">Python</a></li>
                            <li><a class="dropdown-item" href="#javascript">JavaScript</a></li>
                            <li><a class="dropdown-item" href="#java">Java</a></li>
                            <li><hr class="dropdown-divider"></li>
                            <li><h6 class="dropdown-header">其他语言</h6></li>
                            <li><a class="dropdown-item" href="#all-languages">查看全部</a></li>
                        </ul>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#compare">语言比较</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#resources">学习资源</a>
                    </li>
                </ul>
                <div class="d-flex">
                    <div class="input-group me-2">
                        <input type="text" class="form-control" placeholder="搜索语言..." id="searchInput">
                        <button class="btn btn-outline-light" type="button" id="searchButton">
                            <i class="fas fa-search"></i>
                        </button>
                    </div>
                    <button class="btn btn-outline-light me-2" id="themeToggle">
                        <i class="fas fa-moon"></i>
                    </button>
                </div>
            </div>
        </div>
    </nav>

    <!-- 主要内容 -->
    <div class="container mt-4">
        <!-- 搜索和筛选 -->
        <div class="row mb-4 animate__animated animate__fadeIn">
            <div class="col-md-6">
                <div class="input-group">
                    <span class="input-group-text"><i class="fas fa-filter"></i></span>
                    <select class="form-select" id="languageTypeFilter">
                        <option value="all">所有类型</option>
                        <option value="web">Web开发</option>
                        <option value="mobile">移动开发</option>
                        <option value="desktop">桌面应用</option>
                        <option value="data">数据科学</option>
                        <option value="system">系统编程</option>
                        <option value="game">游戏开发</option>
                    </select>
                    <select class="form-select" id="difficultyFilter">
                        <option value="all">所有难度</option>
                        <option value="beginner">初级</option>
                        <option value="intermediate">中级</option>
                        <option value="advanced">高级</option>
                    </select>
                </div>
            </div>
        </div>

        <!-- 语言卡片展示 -->
        <h2 class="mb-4 animate__animated animate__fadeIn" id="all-languages">编程语言</h2>
        <div class="row" id="languagesContainer">
            <!-- 语言卡片将通过JavaScript动态加载 -->
        </div>

        <!-- 语言比较工具 -->
        <div class="mt-5 animate__animated animate__fadeIn" id="compare">
            <h2 class="mb-4">语言比较工具</h2>
            <div class="card">
                <div class="card-body">
                    <div class="row mb-3">
                        <div class="col-md-4">
                            <select class="form-select" id="compareLanguage1">
                                <option value="">选择第一种语言</option>
                            </select>
                        </div>
                        <div class="col-md-4">
                            <select class="form-select" id="compareLanguage2">
                                <option value="">选择第二种语言</option>
                            </select>
                        </div>
                        <div class="col-md-4">
                            <select class="form-select" id="compareLanguage3">
                                <option value="">选择第三种语言(可选)</option>
                            </select>
                        </div>
                    </div>
                    <button class="btn btn-primary" id="compareButton">比较语言</button>
                    <div class="mt-3 comparison-table">
                        <table class="table table-bordered d-none" id="comparisonTable">
                            <thead>
                                <tr>
                                    <th>特性</th>
                                    <th id="compareHeader1">语言1</th>
                                    <th id="compareHeader2">语言2</th>
                                    <th id="compareHeader3" class="d-none">语言3</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr>
                                    <td>类型系统</td>
                                    <td id="typeSystem1"></td>
                                    <td id="typeSystem2"></td>
                                    <td id="typeSystem3" class="d-none"></td>
                                </tr>
                                <tr>
                                    <td>范式</td>
                                    <td id="paradigm1"></td>
                                    <td id="paradigm2"></td>
                                    <td id="paradigm3" class="d-none"></td>
                                </tr>
                                <tr>
                                    <td>性能</td>
                                    <td id="performance1"></td>
                                    <td id="performance2"></td>
                                    <td id="performance3" class="d-none"></td>
                                </tr>
                                <tr>
                                    <td>学习曲线</td>
                                    <td id="learningCurve1"></td>
                                    <td id="learningCurve2"></td>
                                    <td id="learningCurve3" class="d-none"></td>
                                </tr>
                                <tr>
                                    <td>典型用途</td>
                                    <td id="useCase1"></td>
                                    <td id="useCase2"></td>
                                    <td id="useCase3" class="d-none"></td>
                                </tr>
                                <tr>
                                    <td>Hello World 示例</td>
                                    <td><pre id="helloWorld1" class="bg-light p-2 rounded"></pre></td>
                                    <td><pre id="helloWorld2" class="bg-light p-2 rounded"></pre></td>
                                    <td class="d-none"><pre id="helloWorld3" class="bg-light p-2 rounded"></pre></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- 语言详情模态框 -->
    <div class="modal fade" id="languageModal" tabindex="-1" aria-hidden="true">
        <div class="modal-dialog modal-lg">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="modalLanguageTitle"></h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                </div>
                <div class="modal-body">
                    <div class="row">
                        <div class="col-md-4 text-center">
                            <img id="modalLanguageImage" src="" alt="" class="language-icon mb-3">
                            <div class="card mb-3">
                                <div class="card-body">
                                    <h6 class="card-subtitle mb-2 text-muted">基本信息</h6>
                                    <p id="modalLanguageInfo" class="card-text"></p>
                                    <div class="d-flex justify-content-between align-items-center mb-2">
                                        <small class="text-muted">难度:</small>
                                        <span id="modalLanguageDifficulty" class="badge bg-primary"></span>
                                    </div>
                                    <div class="d-flex justify-content-between align-items-center mb-2">
                                        <small class="text-muted">类型:</small>
                                        <span id="modalLanguageType" class="badge bg-success"></span>
                                    </div>
                                    <div class="d-flex justify-content-between align-items-center">
                                        <small class="text-muted">流行度:</small>
                                        <div class="progress progress-tracker w-50">
                                            <div id="modalLanguagePopularity" class="progress-bar bg-info" role="progressbar"></div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                            <div class="card">
                                <div class="card-body">
                                    <h6 class="card-subtitle mb-2 text-muted">官方链接</h6>
                                    <a id="modalLanguageOfficial" href="#" target="_blank" class="btn btn-outline-primary btn-sm w-100 mb-2">
                                        <i class="fas fa-globe me-1"></i> 官方网站
                                    </a>
                                    <a id="modalLanguageDocs" href="#" target="_blank" class="btn btn-outline-secondary btn-sm w-100">
                                        <i class="fas fa-book me-1"></i> 官方文档
                                    </a>
                                </div>
                            </div>
                        </div>
                        <div class="col-md-8">
                            <ul class="nav nav-tabs" id="languageTabs" role="tablist">
                                <li class="nav-item" role="presentation">
                                    <button class="nav-link active" id="roadmap-tab" data-bs-toggle="tab" data-bs-target="#roadmap" type="button">学习路线</button>
                                </li>
                                <li class="nav-item" role="presentation">
                                    <button class="nav-link" id="resources-tab" data-bs-toggle="tab" data-bs-target="#resources" type="button">学习资源</button>
                                </li>
                                <li class="nav-item" role="presentation">
                                    <button class="nav-link" id="community-tab" data-bs-toggle="tab" data-bs-target="#community" type="button">社区</button>
                                </li>
                                <li class="nav-item" role="presentation">
                                    <button class="nav-link" id="projects-tab" data-bs-toggle="tab" data-bs-target="#projects" type="button">项目创意</button>
                                </li>
                            </ul>
                            <div class="tab-content p-3 border border-top-0 rounded-bottom">
                                <div class="tab-pane fade show active" id="roadmap" role="tabpanel">
                                    <div class="accordion" id="roadmapAccordion">
                                        <div class="accordion-item">
                                            <h2 class="accordion-header">
                                                <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#beginnerContent">
                                                    初级学习内容
                                                </button>
                                            </h2>
                                            <div id="beginnerContent" class="accordion-collapse collapse show" data-bs-parent="#roadmapAccordion">
                                                <div class="accordion-body" id="modalBeginnerContent"></div>
                                            </div>
                                        </div>
                                        <div class="accordion-item">
                                            <h2 class="accordion-header">
                                                <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#intermediateContent">
                                                    中级学习内容
                                                </button>
                                            </h2>
                                            <div id="intermediateContent" class="accordion-collapse collapse" data-bs-parent="#roadmapAccordion">
                                                <div class="accordion-body" id="modalIntermediateContent"></div>
                                            </div>
                                        </div>
                                        <div class="accordion-item">
                                            <h2 class="accordion-header">
                                                <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse" data-bs-target="#advancedContent">
                                                    高级学习内容
                                                </button>
                                            </h2>
                                            <div id="advancedContent" class="accordion-collapse collapse" data-bs-parent="#roadmapAccordion">
                                                <div class="accordion-body" id="modalAdvancedContent"></div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                                <div class="tab-pane fade" id="resources" role="tabpanel">
                                    <div class="mb-3">
                                        <h6>免费教程</h6>
                                        <div id="modalTutorials"></div>
                                    </div>
                                    <div class="mb-3">
                                        <h6>推荐书籍</h6>
                                        <div id="modalBooks"></div>
                                    </div>
                                    <div>
                                        <h6>练习平台</h6>
                                        <div id="modalPractice"></div>
                                    </div>
                                </div>
                                <div class="tab-pane fade" id="community" role="tabpanel">
                                    <div id="modalCommunity"></div>
                                </div>
                                <div class="tab-pane fade" id="projects" role="tabpanel">
                                    <div id="modalProjects"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">关闭</button>
                    <button type="button" class="btn btn-primary" id="trackLanguageBtn">跟踪学习进度</button>
                </div>
            </div>
        </div>
    </div>

    <!-- 页脚 -->
    <footer class="bg-dark text-white mt-5 py-4">
        <div class="container">
            <div class="row">
                <div class="col-md-6">
                    <h5><i class="fas fa-code me-2"></i>CodeMaster</h5>
                    <p>一站式编程语言学习资源聚合平台</p>
                    <div class="social-icons">
                        <a href="#" class="text-white me-2"><i class="fab fa-twitter"></i></a>
                        <a href="#" class="text-white me-2"><i class="fab fa-github"></i></a>
                        <a href="#" class="text-white me-2"><i class="fab fa-discord"></i></a>
                    </div>
                </div>
                <div class="col-md-3">
                    <h5>快速链接</h5>
                    <ul class="list-unstyled">
                        <li><a href="#home" class="text-white">首页</a></li>
                        <li><a href="#all-languages" class="text-white">所有语言</a></li>
                        <li><a href="#compare" class="text-white">语言比较</a></li>
                    </ul>
                </div>
                <div class="col-md-3">
                    <h5>关于</h5>
                    <ul class="list-unstyled">
                        <li><a href="#" class="text-white">关于我们</a></li>
                        <li><a href="#" class="text-white">贡献指南</a></li>
                        <li><a href="#" class="text-white">联系我们</a></li>
                    </ul>
                </div>
            </div>
            <hr>
            <div class="text-center">
                <small>© 2023 CodeMaster. 所有资源链接均指向外部网站。</small>
            </div>
        </div>
    </footer>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        // 语言数据 - 12种完整语言数据
        const languagesData = [
            {
                id: "python",
                name: "Python",
                type: ["web", "data", "desktop"],
                difficulty: "beginner",
                popularity: 95,
                description: "Python是一种解释型、高级、通用的编程语言，以其简洁易读的语法而闻名。",
                info: "Python由Guido van Rossum于1991年首次发布。它支持多种编程范式，包括面向对象、命令式、函数式和过程式风格。",
                image: "https://upload.wikimedia.org/wikipedia/commons/thumb/c/c3/Python-logo-notext.svg/1200px-Python-logo-notext.svg.png",
                official: "https://www.python.org",
                docs: "https://docs.python.org/3/",
                roadmap: {
                    beginner: [
                        "基本语法和数据类型",
                        "控制流和函数",
                        "列表、字典等数据结构",
                        "文件操作",
                        "错误和异常处理"
                    ],
                    intermediate: [
                        "面向对象编程",
                        "模块和包",
                        "虚拟环境和包管理",
                        "常用标准库",
                        "基础算法和数据结构"
                    ],
                    advanced: [
                        "装饰器和生成器",
                        "并发和多线程",
                        "网络编程",
                        "元编程",
                        "C扩展开发"
                    ]
                },
                tutorials: [
                    {
                        title: "Python官方教程",
                        url: "https://docs.python.org/3/tutorial/",
                        type: "文档"
                    },
                    {
                        title: "W3Schools Python教程",
                        url: "https://www.w3schools.com/python/",
                        type: "交互式"
                    },
                    {
                        title: "Python全栈教程 - 廖雪峰",
                        url: "https://www.liaoxuefeng.com/wiki/1016959663602400",
                        type: "教程"
                    },
                    {
                        title: "Real Python教程",
                        url: "https://realpython.com/",
                        type: "教程"
                    }
                ],
                books: [
                    {
                        title: "Python Crash Course",
                        author: "Eric Matthes",
                        url: "https://nostarch.com/pythoncrashcourse2e",
                        free: false
                    },
                    {
                        title: "Automate the Boring Stuff with Python",
                        author: "Al Sweigart",
                        url: "https://automatetheboringstuff.com/",
                        free: true
                    },
                    {
                        title: "Fluent Python",
                        author: "Luciano Ramalho",
                        url: "https://www.oreilly.com/library/view/fluent-python-2nd/9781492056348/",
                        free: false
                    }
                ],
                community: [
                    {
                        name: "Python官方论坛",
                        url: "https://discuss.python.org/"
                    },
                    {
                        name: "Stack Overflow Python标签",
                        url: "https://stackoverflow.com/questions/tagged/python"
                    },
                    {
                        name: "Reddit r/Python",
                        url: "https://www.reddit.com/r/Python/"
                    },
                    {
                        name: "Python中文社区",
                        url: "https://www.python.org.cn/"
                    }
                ],
                practice: [
                    {
                        name: "LeetCode Python问题",
                        url: "https://leetcode.com/tag/python/"
                    },
                    {
                        name: "HackerRank Python教程",
                        url: "https://www.hackerrank.com/domains/tutorials/10-days-of-python"
                    },
                    {
                        name: "Codewars Python练习",
                        url: "https://www.codewars.com/?language=python"
                    }
                ],
                projects: [
                    "创建一个天气查询应用",
                    "开发一个简单的博客系统",
                    "构建数据分析仪表板",
                    "制作自动化文件整理工具",
                    "开发一个简单的网络爬虫"
                ],
                comparison: {
                    typeSystem: "动态类型",
                    paradigm: "多范式(面向对象, 函数式, 过程式)",
                    performance: "中等",
                    learningCurve: "平缓",
                    useCase: "Web开发, 数据分析, 人工智能, 脚本",
                    helloWorld: "print('Hello, World!')"
                }
            },
            {
                id: "javascript",
                name: "JavaScript",
                type: ["web"],
                difficulty: "beginner",
                popularity: 90,
                description: "JavaScript是一种轻量级的解释型编程语言，主要用于Web开发。",
                info: "JavaScript由Brendan Eich于1995年创建，最初是为了在浏览器中添加交互性。现在它也可以用于服务器端(Node.js)和移动应用开发。",
                image: "https://upload.wikimedia.org/wikipedia/commons/6/6a/JavaScript-logo.png",
                official: "https://developer.mozilla.org/en-US/docs/Web/JavaScript",
                docs: "https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference",
                roadmap: {
                    beginner: [
                        "基本语法和数据类型",
                        "DOM操作",
                        "事件处理",
                        "函数和作用域",
                        "ES6基础(let/const, 箭头函数)"
                    ],
                    intermediate: [
                        "异步编程(回调, Promise, async/await)",
                        "面向对象编程",
                        "模块系统",
                        "常见设计模式",
                        "API调用和AJAX"
                    ],
                    advanced: [
                        "闭包和原型链",
                        "性能优化",
                        "Web Workers",
                        "TypeScript",
                        "框架深入(Vue/React/Angular)"
                    ]
                },
                tutorials: [
                    {
                        title: "MDN JavaScript指南",
                        url: "https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide",
                        type: "文档"
                    },
                    {
                        title: "JavaScript.info",
                        url: "https://javascript.info/",
                        type: "教程"
                    },
                    {
                        title: "Eloquent JavaScript",
                        url: "https://eloquentjavascript.net/",
                        type: "书籍/教程"
                    },
                    {
                        title: "freeCodeCamp JavaScript课程",
                        url: "https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/",
                        type: "交互式"
                    }
                ],
                books: [
                    {
                        title: "You Don't Know JS",
                        author: "Kyle Simpson",
                        url: "https://github.com/getify/You-Dont-Know-JS",
                        free: true
                    },
                    {
                        title: "JavaScript: The Good Parts",
                        author: "Douglas Crockford",
                        url: "https://www.oreilly.com/library/view/javascript-the-good/9780596517748/",
                        free: false
                    },
                    {
                        title: "Eloquent JavaScript",
                        author: "Marijn Haverbeke",
                        url: "https://eloquentjavascript.net/",
                        free: true
                    }
                ],
                community: [
                    {
                        name: "Stack Overflow JavaScript标签",
                        url: "https://stackoverflow.com/questions/tagged/javascript"
                    },
                    {
                        name: "Dev.to JavaScript标签",
                        url: "https://dev.to/t/javascript"
                    },
                    {
                        name: "Reddit r/javascript",
                        url: "https://www.reddit.com/r/javascript/"
                    },
                    {
                        name: "JavaScript中文网",
                        url: "https://www.javascriptcn.com/"
                    }
                ],
                practice: [
                    {
                        name: "Codewars JavaScript问题",
                        url: "https://www.codewars.com/?language=javascript"
                    },
                    {
                        name: "Frontend Mentor",
                        url: "https://www.frontendmentor.io/"
                    },
                    {
                        name: "JS Challenger",
                        url: "https://www.jschallenger.com/"
                    }
                ],
                projects: [
                    "创建一个待办事项应用",
                    "开发一个简单的游戏(如井字棋)",
                    "构建天气应用",
                    "制作Chrome扩展",
                    "开发一个简单的单页应用"
                ],
                comparison: {
                    typeSystem: "动态类型",
                    paradigm: "多范式(面向对象, 函数式, 过程式)",
                    performance: "中等(浏览器中)",
                    learningCurve: "入门易, 精通难",
                    useCase: "Web前端, 服务器端(Node.js), 移动应用",
                    helloWorld: "console.log('Hello, World!');"
                }
            },
            {
                id: "java",
                name: "Java",
                type: ["web", "mobile", "desktop"],
                difficulty: "intermediate",
                popularity: 85,
                description: `Java是一种面向对象的编程语言，以其"一次编写，到处运行"的特性而闻名。`,
                info: "Java由Sun Microsystems于1995年发布，现在是Oracle公司的一部分。它是一种静态类型语言，广泛应用于企业级应用和Android开发。",
                image: "https://upload.wikimedia.org/wikipedia/en/3/30/Java_programming_language_logo.svg",
                official: "https://www.java.com",
                docs: "https://docs.oracle.com/en/java/",
                roadmap: {
                    beginner: [
                        "基本语法和数据类型",
                        "面向对象编程基础",
                        "异常处理",
                        "集合框架",
                        "输入/输出操作"
                    ],
                    intermediate: [
                        "多线程编程",
                        "网络编程",
                        "JDBC和数据库连接",
                        "设计模式",
                        "Java 8+新特性"
                    ],
                    advanced: [
                        "JVM内部机制",
                        "性能优化",
                        "Spring框架",
                        "微服务架构",
                        "响应式编程"
                    ]
                },
                tutorials: [
                    {
                        title: "Java官方教程",
                        url: "https://docs.oracle.com/javase/tutorial/",
                        type: "文档"
                    },
                    {
                        title: "W3Schools Java教程",
                        url: "https://www.w3schools.com/java/",
                        type: "交互式"
                    },
                    {
                        title: "Java编程思想 - 廖雪峰",
                        url: "https://www.liaoxuefeng.com/wiki/1252599548343744",
                        type: "教程"
                    },
                    {
                        title: "Baeldung Java教程",
                        url: "https://www.baeldung.com/",
                        type: "教程"
                    }
                ],
                books: [
                    {
                        title: "Effective Java",
                        author: "Joshua Bloch",
                        url: "https://www.oreilly.com/library/view/effective-java-3rd/9780134686097/",
                        free: false
                    },
                    {
                        title: "Head First Java",
                        author: "Kathy Sierra & Bert Bates",
                        url: "https://www.oreilly.com/library/view/head-first-java/0596009208/",
                        free: false
                    },
                    {
                        title: "Java核心技术卷I",
                        author: "Cay S. Horstmann",
                        url: "https://horstmann.com/corejava/",
                        free: false
                    }
                ],
                community: [
                    {
                        name: "Stack Overflow Java标签",
                        url: "https://stackoverflow.com/questions/tagged/java"
                    },
                    {
                        name: "Reddit r/java",
                        url: "https://www.reddit.com/r/java/"
                    },
                    {
                        name: "Java官方社区",
                        url: "https://community.oracle.com/community/developer-content/java/"
                    },
                    {
                        name: "Java中文网",
                        url: "https://www.java1234.com/"
                    }
                ],
                practice: [
                    {
                        name: "LeetCode Java问题",
                        url: "https://leetcode.com/tag/java/"
                    },
                    {
                        name: "CodingBat Java练习",
                        url: "https://codingbat.com/java"
                    },
                    {
                        name: "HackerRank Java教程",
                        url: "https://www.hackerrank.com/domains/tutorials/10-days-of-java"
                    }
                ],
                projects: [
                    "开发一个简单的银行系统",
                    "创建一个学生管理系统",
                    "构建一个聊天应用",
                    "开发一个简单的游戏(如贪吃蛇)",
                    "制作一个文件加密工具"
                ],
                comparison: {
                    typeSystem: "静态强类型",
                    paradigm: "面向对象",
                    performance: "高性能",
                    learningCurve: "中等",
                    useCase: "企业应用, Android开发, 后端服务",
                    helloWorld: "public class HelloWorld {\n    public static void main(String[] args) {\n        System.out.println(\"Hello, World!\");\n    }\n}"
                }
            },
            {
                id: "csharp",
                name: "C#",
                type: ["web", "desktop", "game"],
                difficulty: "intermediate",
                popularity: 80,
                description: "C#是由微软开发的面向对象的编程语言，运行在.NET框架上。",
                info: "C#由Anders Hejlsberg和他的团队在2000年开发，结合了C++的强大功能和Visual Basic的简单性。广泛用于Windows应用和游戏开发(Unity)。",
                image: "https://upload.wikimedia.org/wikipedia/commons/4/4f/Csharp_Logo.png",
                official: "https://docs.microsoft.com/en-us/dotnet/csharp/",
                docs: "https://docs.microsoft.com/en-us/dotnet/csharp/",
                roadmap: {
                    beginner: [
                        "基本语法和数据类型",
                        "面向对象编程基础",
                        "异常处理",
                        "集合和泛型",
                        "LINQ基础"
                    ],
                    intermediate: [
                        "异步编程(async/await)",
                        "委托和事件",
                        "反射和特性",
                        "文件I/O和序列化",
                        "Entity Framework"
                    ],
                    advanced: [
                        ".NET Core/5+新特性",
                        "微服务架构",
                        "性能优化",
                        "跨平台开发",
                        "Unity游戏开发"
                    ]
                },
                tutorials: [
                    {
                        title: "微软C#文档",
                        url: "https://docs.microsoft.com/en-us/dotnet/csharp/",
                        type: "文档"
                    },
                    {
                        title: "W3Schools C#教程",
                        url: "https://www.w3schools.com/cs/index.php",
                        type: "交互式"
                    },
                    {
                        title: "C# Station教程",
                        url: "https://www.csharp-station.com/tutorial.aspx",
                        type: "教程"
                    },
                    {
                        title: "TutorialsTeacher C#教程",
                        url: "https://www.tutorialsteacher.com/csharp",
                        type: "教程"
                    }
                ],
                books: [
                    {
                        title: "C# in Depth",
                        author: "Jon Skeet",
                        url: "https://www.manning.com/books/c-sharp-in-depth-fourth-edition",
                        free: false
                    },
                    {
                        title: "Head First C#",
                        author: "Andrew Stellman & Jennifer Greene",
                        url: "https://www.oreilly.com/library/view/head-first-c/9781449358846/",
                        free: false
                    },
                    {
                        title: "C# 9.0 in a Nutshell",
                        author: "Joseph Albahari",
                        url: "https://www.oreilly.com/library/view/c-90-in/9781098100964/",
                        free: false
                    }
                ],
                community: [
                    {
                        name: "Stack Overflow C#标签",
                        url: "https://stackoverflow.com/questions/tagged/c%23"
                    },
                    {
                        name: "Reddit r/csharp",
                        url: "https://www.reddit.com/r/csharp/"
                    },
                    {
                        name: "C# Corner",
                        url: "https://www.c-sharpcorner.com/"
                    },
                    {
                        name: "微软开发者社区",
                        url: "https://developercommunity.visualstudio.com/"
                    }
                ],
                practice: [
                    {
                        name: "Exercism C#学习路径",
                        url: "https://exercism.org/tracks/csharp"
                    },
                    {
                        name: "Codewars C#问题",
                        url: "https://www.codewars.com/?language=csharp"
                    },
                    {
                        name: "LeetCode C#问题",
                        url: "https://leetcode.com/tag/csharp/"
                    }
                ],
                projects: [
                    "开发一个Windows窗体应用",
                    "创建一个简单的库存管理系统",
                    "构建一个ASP.NET Core Web应用",
                    "开发一个Unity小游戏",
                    "制作一个文件压缩工具"
                ],
                comparison: {
                    typeSystem: "静态强类型",
                    paradigm: "面向对象, 函数式",
                    performance: "高性能",
                    learningCurve: "中等",
                    useCase: "Windows应用, 游戏开发, Web服务",
                    helloWorld: "using System;\n\nclass HelloWorld {\n    static void Main() {\n        Console.WriteLine(\"Hello, World!\");\n    }\n}"
                }
            },
            {
                id: "cpp",
                name: "C++",
                type: ["system", "game", "desktop"],
                difficulty: "advanced",
                popularity: 75,
                description: "C++是一种通用的编程语言，支持过程化、面向对象和泛型编程。",
                info: "C++由Bjarne Stroustrup于1985年作为C语言的扩展而开发。它以高性能著称，广泛用于系统/应用软件、游戏引擎和嵌入式系统。",
                image: "https://upload.wikimedia.org/wikipedia/commons/1/18/ISO_C%2B%2B_Logo.svg",
                official: "https://isocpp.org/",
                docs: "https://en.cppreference.com/w/",
                roadmap: {
                    beginner: [
                        "基本语法和数据类型",
                        "指针和引用",
                        "函数和类",
                        "标准模板库(STL)基础",
                        "内存管理基础"
                    ],
                    intermediate: [
                        "模板和泛型编程",
                        "运算符重载",
                        "异常处理",
                        "多线程编程",
                        "设计模式"
                    ],
                    advanced: [
                        "移动语义和完美转发",
                        "元编程和constexpr",
                        "性能优化技术",
                        "低级系统编程",
                        "现代C++(C++11/14/17/20)"
                    ]
                },
                tutorials: [
                    {
                        title: "C++官方参考",
                        url: "https://en.cppreference.com/w/",
                        type: "文档"
                    },
                    {
                        title: "LearnCpp.com",
                        url: "https://www.learncpp.com/",
                        type: "教程"
                    },
                    {
                        title: "C++教程 - 菜鸟教程",
                        url: "https://www.runoob.com/cplusplus/cpp-tutorial.html",
                        type: "教程"
                    },
                    {
                        title: "Google C++风格指南",
                        url: "https://google.github.io/styleguide/cppguide.html",
                        type: "最佳实践"
                    }
                ],
                books: [
                    {
                        title: "The C++ Programming Language",
                        author: "Bjarne Stroustrup",
                        url: "https://www.stroustrup.com/4th.html",
                        free: false
                    },
                    {
                        title: "Effective Modern C++",
                        author: "Scott Meyers",
                        url: "https://www.oreilly.com/library/view/effective-modern-c/9781491908419/",
                        free: false
                    },
                    {
                        title: "C++ Primer",
                        author: "Stanley B. Lippman",
                        url: "https://www.oreilly.com/library/view/c-primer-fifth/9780133053043/",
                        free: false
                    }
                ],
                community: [
                    {
                        name: "Stack Overflow C++标签",
                        url: "https://stackoverflow.com/questions/tagged/c%2b%2b"
                    },
                    {
                        name: "Reddit r/cpp",
                        url: "https://www.reddit.com/r/cpp/"
                    },
                    {
                        name: "C++论坛",
                        url: "https://cplusplus.com/forum/"
                    },
                    {
                        name: "C++中文网",
                        url: "https://c.biancheng.net/cpp/"
                    }
                ],
                practice: [
                    {
                        name: "LeetCode C++问题",
                        url: "https://leetcode.com/tag/cpp/"
                    },
                    {
                        name: "HackerRank C++教程",
                        url: "https://www.hackerrank.com/domains/tutorials/10-days-of-cpp"
                    },
                    {
                        name: "CodeChef C++问题",
                        url: "https://www.codechef.com/problems/school/?itm_medium=navmenu&itm_campaign=problems_head"
                    }
                ],
                projects: [
                    "开发一个简单的游戏引擎组件",
                    "创建一个高性能计算应用",
                    "构建一个命令行工具",
                    "开发一个内存分配器",
                    "制作一个简单的操作系统内核"
                ],
                comparison: {
                    typeSystem: "静态强类型",
                    paradigm: "多范式(过程式, 面向对象, 泛型)",
                    performance: "极高",
                    learningCurve: "陡峭",
                    useCase: "系统编程, 游戏开发, 高性能计算",
                    helloWorld: "#include <iostream>\n\nint main() {\n    std::cout << \"Hello, World!\";\n    return 0;\n}"
                }
            },
            {
                id: "go",
                name: "Go (Golang)",
                type: ["web", "system"],
                difficulty: "intermediate",
                popularity: 70,
                description: "Go是由Google开发的一种静态类型、编译型语言，强调简洁和高并发。",
                info: "Go由Robert Griesemer、Rob Pike和Ken Thompson于2009年设计。它结合了动态语言的易用性和静态语言的安全性与性能，特别适合网络服务和分布式系统。",
                image: "https://upload.wikimedia.org/wikipedia/commons/0/05/Go_Logo_Blue.svg",
                official: "https://golang.org/",
                docs: "https://golang.org/doc/",
                roadmap: {
                    beginner: [
                        "基本语法和数据类型",
                        "函数和方法",
                        "接口和结构体",
                        "错误处理",
                        "包管理"
                    ],
                    intermediate: [
                        "并发编程(goroutines和channels)",
                        "标准库使用",
                        "Web服务开发",
                        "测试和性能分析",
                        "与C的互操作性"
                    ],
                    advanced: [
                        "高级并发模式",
                        "性能优化",
                        "反射和元编程",
                        "插件系统",
                        "编译器内部机制"
                    ]
                },
                tutorials: [
                    {
                        title: "Go官方教程",
                        url: "https://golang.org/doc/tutorial/",
                        type: "文档"
                    },
                    {
                        title: "A Tour of Go",
                        url: "https://tour.golang.org/welcome/1",
                        type: "交互式"
                    },
                    {
                        title: "Go by Example",
                        url: "https://gobyexample.com/",
                        type: "示例"
                    },
                    {
                        title: "Go语言圣经",
                        url: "https://books.studygolang.com/gopl-zh/",
                        type: "教程"
                    }
                ],
                books: [
                    {
                        title: "The Go Programming Language",
                        author: "Alan A. A. Donovan & Brian W. Kernighan",
                        url: "https://www.gopl.io/",
                        free: false
                    },
                    {
                        title: "Go Web Programming",
                        author: "Sau Sheong Chang",
                        url: "https://www.manning.com/books/go-web-programming",
                        free: false
                    },
                    {
                        title: "Learning Go",
                        author: "Jon Bodner",
                        url: "https://www.oreilly.com/library/view/learning-go/9781492077206/",
                        free: false
                    }
                ],
                community: [
                    {
                        name: "Go官方论坛",
                        url: "https://forum.golangbridge.org/"
                    },
                    {
                        name: "Stack Overflow Go标签",
                        url: "https://stackoverflow.com/questions/tagged/go"
                    },
                    {
                        name: "Reddit r/golang",
                        url: "https://www.reddit.com/r/golang/"
                    },
                    {
                        name: "Go语言中文网",
                        url: "https://studygolang.com/"
                    }
                ],
                practice: [
                    {
                        name: "Exercism Go学习路径",
                        url: "https://exercism.org/tracks/go"
                    },
                    {
                        name: "Codewars Go问题",
                        url: "https://www.codewars.com/?language=go"
                    },
                    {
                        name: "LeetCode Go问题",
                        url: "https://leetcode.com/tag/golang/"
                    }
                ],
                projects: [
                    "开发一个简单的Web服务",
                    "创建一个并发爬虫",
                    "构建一个CLI工具",
                    "开发一个微服务",
                    "制作一个简单的区块链实现"
                ],
                comparison: {
                    typeSystem: "静态强类型",
                    paradigm: "命令式, 结构化",
                    performance: "高性能",
                    learningCurve: "中等",
                    useCase: "网络服务, 分布式系统, 云原生应用",
                    helloWorld: "package main\n\nimport \"fmt\"\n\nfunc main() {\n    fmt.Println(\"Hello, World!\")\n}"
                }
            },
            {
                id: "rust",
                name: "Rust",
                type: ["system"],
                difficulty: "advanced",
                popularity: 65,
                description: "Rust是一种专注于安全、性能和并发性的系统编程语言。",
                info: "Rust由Mozilla Research开发，首次发布于2010年。它提供了内存安全保证而无需垃圾回收，并支持函数式、并发和面向对象的编程风格。",
                image: "https://upload.wikimedia.org/wikipedia/commons/thumb/d/d5/Rust_programming_language_black_logo.svg/1200px-Rust_programming_language_black_logo.svg.png",
                official: "https://www.rust-lang.org",
                docs: "https://doc.rust-lang.org/book/",
                roadmap: {
                    beginner: [
                        "基本语法和数据类型",
                        "所有权和借用",
                        "结构体和枚举",
                        "模式匹配",
                        "错误处理"
                    ],
                    intermediate: [
                        "生命周期",
                        "特质和泛型",
                        "并发编程",
                        "宏",
                        "常用库(crates)"
                    ],
                    advanced: [
                        "不安全Rust",
                        "FFI(外部函数接口)",
                        "编译器插件",
                        "嵌入式开发",
                        "性能优化"
                    ]
                },
                tutorials: [
                    {
                        title: "Rust官方教程",
                        url: "https://doc.rust-lang.org/book/",
                        type: "文档"
                    },
                    {
                        title: "Rust By Example",
                        url: "https://doc.rust-lang.org/rust-by-example/",
                        type: "交互式"
                    },
                    {
                        title: "Rustlings小练习",
                        url: "https://github.com/rust-lang/rustlings",
                        type: "练习"
                    },
                    {
                        title: "Rust语言圣经",
                        url: "https://course.rs/",
                        type: "教程"
                    }
                ],
                books: [
                    {
                        title: "The Rust Programming Language",
                        author: "Steve Klabnik and Carol Nichols",
                        url: "https://doc.rust-lang.org/book/",
                        free: true
                    },
                    {
                        title: "Rust in Action",
                        author: "Tim McNamara",
                        url: "https://www.manning.com/books/rust-in-action",
                        free: false
                    },
                    {
                        title: "Programming Rust",
                        author: "Jim Blandy & Jason Orendorff",
                        url: "https://www.oreilly.com/library/view/programming-rust-2nd/9781492052586/",
                        free: false
                    }
                ],
                community: [
                    {
                        name: "Rust官方用户论坛",
                        url: "https://users.rust-lang.org/"
                    },
                    {
                        name: "Stack Overflow Rust标签",
                        url: "https://stackoverflow.com/questions/tagged/rust"
                    },
                    {
                        name: "Reddit r/rust",
                        url: "https://www.reddit.com/r/rust/"
                    },
                    {
                        name: "Rust中文社区",
                        url: "https://rustcc.cn/"
                    }
                ],
                practice: [
                    {
                        name: "Rustlings练习",
                        url: "https://github.com/rust-lang/rustlings"
                    },
                    {
                        name: "Exercism Rust学习路径",
                        url: "https://exercism.org/tracks/rust"
                    },
                    {
                        name: "LeetCode Rust问题",
                        url: "https://leetcode.com/tag/rust/"
                    }
                ],
                projects: [
                    "创建一个命令行工具",
                    "开发一个简单的Web服务器",
                    "构建一个解析器或编译器",
                    "制作一个游戏引擎组件",
                    "开发一个系统监控工具"
                ],
                comparison: {
                    typeSystem: "静态强类型",
                    paradigm: "多范式(函数式, 面向对象)",
                    performance: "高性能(接近C/C++)",
                    learningCurve: "陡峭",
                    useCase: "系统编程, 嵌入式, 高性能应用",
                    helloWorld: "fn main() {\n    println!(\"Hello, World!\");\n}"
                }
            },
            {
                id: "swift",
                name: "Swift",
                type: ["mobile", "desktop"],
                difficulty: "intermediate",
                popularity: 70,
                description: "Swift是Apple开发的用于iOS、macOS等平台的编程语言，结合了性能和开发效率。",
                info: "Swift由Apple于2014年发布，旨在替代Objective-C。它是一种安全、快速和互动的语言，支持现代编程概念如协议和泛型。",
                image: "https://bkimg.cdn.bcebos.com/pic/a6efce1b9d16fdfaaf51033032c59b5494eef11fcd90?x-bce-process=image/format,f_auto/quality,Q_70/resize,m_lfit,limit_1,w_536",
                official: "https://swift.org/",
                docs: "https://docs.swift.org/swift-book/",
                roadmap: {
                    beginner: [
                        "基本语法和数据类型",
                        "可选类型和错误处理",
                        "函数和闭包",
                        "结构体和类",
                        "协议基础"
                    ],
                    intermediate: [
                        "泛型编程",
                        "内存管理和ARC",
                        "并发编程",
                        "SwiftUI基础",
                        "与Objective-C互操作"
                    ],
                    advanced: [
                        "高级SwiftUI",
                        "性能优化",
                        "编译器内部机制",
                        "服务器端Swift",
                        "跨平台开发"
                    ]
                },
                tutorials: [
                    {
                        title: "Swift官方教程",
                        url: "https://docs.swift.org/swift-book/",
                        type: "文档"
                    },
                    {
                        title: "Swift Playgrounds",
                        url: "https://www.apple.com/swift/playgrounds/",
                        type: "交互式"
                    },
                    {
                        title: "Hacking with Swift",
                        url: "https://www.hackingwithswift.com/",
                        type: "教程"
                    },
                    {
                        title: "Ray Wenderlich Swift教程",
                        url: "https://www.raywenderlich.com/swift",
                        type: "教程"
                    }
                ],
                books: [
                    {
                        title: "The Swift Programming Language",
                        author: "Apple Inc.",
                        url: "https://books.apple.com/us/book/the-swift-programming-language/id881256329",
                        free: true
                    },
                    {
                        title: "SwiftUI by Tutorials",
                        author: "Ray Wenderlich Team",
                        url: "https://www.raywenderlich.com/books/swiftui-by-tutorials",
                        free: false
                    },
                    {
                        title: "Advanced Swift",
                        author: "Chris Eidhof & Ole Begemann",
                        url: "https://www.objc.io/books/advanced-swift/",
                        free: false
                    }
                ],
                community: [
                    {
                        name: "Swift官方论坛",
                        url: "https://forums.swift.org/"
                    },
                    {
                        name: "Stack Overflow Swift标签",
                        url: "https://stackoverflow.com/questions/tagged/swift"
                    },
                    {
                        name: "Reddit r/swift",
                        url: "https://www.reddit.com/r/swift/"
                    },
                    {
                        name: "SwiftGG中文站",
                        url: "https://swiftgg.gitbook.io/"
                    }
                ],
                practice: [
                    {
                        name: "LeetCode Swift问题",
                        url: "https://leetcode.com/tag/swift/"
                    },
                    {
                        name: "HackerRank Swift教程",
                        url: "https://www.hackerrank.com/domains/tutorials/10-days-of-swift"
                    },
                    {
                        name: "Exercism Swift学习路径",
                        url: "https://exercism.org/tracks/swift"
                    }
                ],
                projects: [
                    "开发一个iOS天气应用",
                    "创建一个macOS笔记应用",
                    "构建一个简单的游戏",
                    "开发一个AR应用",
                    "制作一个健康追踪应用"
                ],
                comparison: {
                    typeSystem: "静态强类型",
                    paradigm: "多范式(面向对象, 函数式, 协议导向)",
                    performance: "高性能",
                    learningCurve: "中等",
                    useCase: "iOS/macOS应用开发, 服务器端",
                    helloWorld: "print(\"Hello, World!\")"
                }
            },
            {
                id: "kotlin",
                name: "Kotlin",
                type: ["mobile", "web"],
                difficulty: "intermediate",
                popularity: 75,
                description: "Kotlin是一种现代、简洁的编程语言，可编译为JVM字节码、JavaScript或原生代码。",
                info: "Kotlin由JetBrains于2011年开发，2017年被Google宣布为Android开发的官方语言。它与Java完全互操作，同时提供了更现代的语法和特性。",
                image: "https://upload.wikimedia.org/wikipedia/commons/7/74/Kotlin_Icon.png",
                official: "https://kotlinlang.org/",
                docs: "https://kotlinlang.org/docs/home.html",
                roadmap: {
                    beginner: [
                        "基本语法和数据类型",
                        "函数和lambda表达式",
                        "空安全和异常处理",
                        "类和对象",
                        "集合操作"
                    ],
                    intermediate: [
                        "扩展函数和属性",
                        "协程和异步编程",
                        "DSL构建",
                        "与Java互操作",
                        "Android开发基础"
                    ],
                    advanced: [
                        "多平台开发",
                        "编译器插件",
                        "性能优化",
                        "高级协程使用",
                        "Kotlin/Native"
                    ]
                },
                tutorials: [
                    {
                        title: "Kotlin官方教程",
                        url: "https://kotlinlang.org/docs/home.html",
                        type: "文档"
                    },
                    {
                        title: "Kotlin Koans",
                        url: "https://play.kotlinlang.org/koans",
                        type: "交互式"
                    },
                    {
                        title: "Kotlin for Android Developers",
                        url: "https://developer.android.com/kotlin",
                        type: "教程"
                    },
                    {
                        title: "Kotlin语言中文站",
                        url: "https://www.kotlincn.net/",
                        type: "教程"
                    }
                ],
                books: [
                    {
                        title: "Kotlin in Action",
                        author: "Dmitry Jemerov & Svetlana Isakova",
                        url: "https://www.manning.com/books/kotlin-in-action",
                        free: false
                    },
                    {
                        title: "Head First Kotlin",
                        author: "Dawn Griffiths & David Griffiths",
                        url: "https://www.oreilly.com/library/view/head-first-kotlin/9781491996683/",
                        free: false
                    },
                    {
                        title: "Atomic Kotlin",
                        author: "Bruce Eckel & Svetlana Isakova",
                        url: "https://www.atomickotlin.com/",
                        free: false
                    }
                ],
                community: [
                    {
                        name: "Kotlin官方论坛",
                        url: "https://discuss.kotlinlang.org/"
                    },
                    {
                        name: "Stack Overflow Kotlin标签",
                        url: "https://stackoverflow.com/questions/tagged/kotlin"
                    },
                    {
                        name: "Reddit r/kotlin",
                        url: "https://www.reddit.com/r/Kotlin/"
                    },
                    {
                        name: "Kotlin中文社区",
                        url: "https://www.kotliner.cn/"
                    }
                ],
                practice: [
                    {
                        name: "Exercism Kotlin学习路径",
                        url: "https://exercism.org/tracks/kotlin"
                    },
                    {
                        name: "Codewars Kotlin问题",
                        url: "https://www.codewars.com/?language=kotlin"
                    },
                    {
                        name: "LeetCode Kotlin问题",
                        url: "https://leetcode.com/tag/kotlin/"
                    }
                ],
                projects: [
                    "开发一个Android应用",
                    "创建一个后端服务",
                    "构建一个多平台应用",
                    "开发一个DSL",
                    "制作一个简单的游戏"
                ],
                comparison: {
                    typeSystem: "静态强类型",
                    paradigm: "多范式(面向对象, 函数式)",
                    performance: "高性能(与Java相当)",
                    learningCurve: "中等",
                    useCase: "Android开发, 后端服务, 多平台应用",
                    helloWorld: "fun main() {\n    println(\"Hello, World!\")\n}"
                }
            },
            {
                id: "typescript",
                name: "TypeScript",
                type: ["web"],
                difficulty: "intermediate",
                popularity: 80,
                description: "TypeScript是JavaScript的超集，添加了静态类型定义。",
                info: "TypeScript由Microsoft于2012年开发，编译为纯JavaScript。它为大型应用开发提供了更好的工具支持和代码可维护性。",
                image: "https://upload.wikimedia.org/wikipedia/commons/4/4c/Typescript_logo_2020.svg",
                official: "https://www.typescriptlang.org/",
                docs: "https://www.typescriptlang.org/docs/",
                roadmap: {
                    beginner: [
                        "基本类型和接口",
                        "类和继承",
                        "模块系统",
                        "类型推断",
                        "与JavaScript互操作"
                    ],
                    intermediate: [
                        "高级类型(联合、交叉、条件类型)",
                        "泛型编程",
                        "装饰器",
                        "类型声明文件(.d.ts)",
                        "工具链配置"
                    ],
                    advanced: [
                        "类型编程",
                        "编译器API",
                        "性能优化",
                        "框架集成(React, Vue等)",
                        "自定义转换器"
                    ]
                },
                tutorials: [
                    {
                        title: "TypeScript官方教程",
                        url: "https://www.typescriptlang.org/docs/",
                        type: "文档"
                    },
                    {
                        title: "TypeScript Deep Dive",
                        url: "https://basarat.gitbook.io/typescript/",
                        type: "教程"
                    },
                    {
                        title: "TypeScript入门教程",
                        url: "https://ts.xcatliu.com/",
                        type: "教程"
                    },
                    {
                        title: "Total TypeScript",
                        url: "https://www.totaltypescript.com/",
                        type: "教程"
                    }
                ],
                books: [
                    {
                        title: "Programming TypeScript",
                        author: "Boris Cherny",
                        url: "https://www.oreilly.com/library/view/programming-typescript/9781492037644/",
                        free: false
                    },
                    {
                        title: "Effective TypeScript",
                        author: "Dan Vanderkam",
                        url: "https://effectivetypescript.com/",
                        free: false
                    },
                    {
                        title: "TypeScript Quickly",
                        author: "Yakov Fain & Anton Moiseev",
                        url: "https://www.manning.com/books/typescript-quickly",
                        free: false
                    }
                ],
                community: [
                    {
                        name: "TypeScript官方社区",
                        url: "https://github.com/microsoft/TypeScript/discussions"
                    },
                    {
                        name: "Stack Overflow TypeScript标签",
                        url: "https://stackoverflow.com/questions/tagged/typescript"
                    },
                    {
                        name: "Reddit r/typescript",
                        url: "https://www.reddit.com/r/typescript/"
                    },
                    {
                        name: "TypeScript中文网",
                        url: "https://www.tslang.cn/"
                    }
                ],
                practice: [
                    {
                        name: "Type Challenges",
                        url: "https://github.com/type-challenges/type-challenges"
                    },
                    {
                        name: "LeetCode TypeScript问题",
                        url: "https://leetcode.com/tag/typescript/"
                    },
                    {
                        name: "Codewars TypeScript问题",
                        url: "https://www.codewars.com/?language=typescript"
                    }
                ],
                projects: [
                    "开发一个React/Vue应用",
                    "创建一个Node.js后端服务",
                    "构建一个CLI工具",
                    "开发一个浏览器扩展",
                    "制作一个简单的游戏"
                ],
                comparison: {
                    typeSystem: "静态类型(可选的)",
                    paradigm: "多范式(面向对象, 函数式)",
                    performance: "与JavaScript相同(编译后)",
                    learningCurve: "中等(需JavaScript基础)",
                    useCase: "大型前端应用, 全栈开发",
                    helloWorld: "console.log('Hello, World!');"
                }
            },
            {
                id: "dart",
                name: "Dart",
                type: ["mobile", "web"],
                difficulty: "intermediate",
                popularity: 65,
                description: "Dart是Google开发的面向对象的语言，用于构建跨平台应用(Flutter)。",
                info: "Dart由Google于2011年开发，2018年随着Flutter的流行而受到关注。它可以编译为原生代码或JavaScript，支持JIT和AOT编译。",
                image: "https://upload.wikimedia.org/wikipedia/commons/7/7e/Dart-logo.png",
                official: "https://dart.dev/",
                docs: "https://dart.dev/guides",
                roadmap: {
                    beginner: [
                        "基本语法和数据类型",
                        "函数和类",
                        "异步编程(async/await)",
                        "集合和泛型",
                        "错误处理"
                    ],
                    intermediate: [
                        "Flutter框架基础",
                        "状态管理",
                        "平台特定代码",
                        "测试和调试",
                        "包管理"
                    ],
                    advanced: [
                        "性能优化",
                        "自定义绘制和动画",
                        "插件开发",
                        "Web和桌面应用",
                        "编译器内部机制"
                    ]
                },
                tutorials: [
                    {
                        title: "Dart官方教程",
                        url: "https://dart.dev/guides",
                        type: "文档"
                    },
                    {
                        title: "Dart Pad",
                        url: "https://dartpad.dev/",
                        type: "交互式"
                    },
                    {
                        title: "Flutter官方文档",
                        url: "https://flutter.dev/docs",
                        type: "教程"
                    },
                    {
                        title: "Dart语言中文网",
                        url: "https://dart.cn/",
                        type: "教程"
                    }
                ],
                books: [
                    {
                        title: "Dart in Action",
                        author: "Manning Publications",
                        url: "https://www.manning.com/books/dart-in-action",
                        free: false
                    },
                    {
                        title: "Flutter in Action",
                        author: "Eric Windmill",
                        url: "https://www.manning.com/books/flutter-in-action",
                        free: false
                    },
                    {
                        title: "Beginning Flutter",
                        author: "Marco L. Napoli",
                        url: "https://www.wiley.com/en-us/Beginning+Flutter%3A+A+Hands+On+Guide+to+App+Development-p-9781119550859",
                        free: false
                    }
                ],
                community: [
                    {
                        name: "Dart官方社区",
                        url: "https://groups.google.com/g/dart-dev"
                    },
                    {
                        name: "Stack Overflow Dart标签",
                        url: "https://stackoverflow.com/questions/tagged/dart"
                    },
                    {
                        name: "Reddit r/dartlang",
                        url: "https://www.reddit.com/r/dartlang/"
                    },
                    {
                        name: "Flutter中文社区",
                        url: "https://flutter.cn/"
                    }
                ],
                practice: [
                    {
                        name: "Exercism Dart学习路径",
                        url: "https://exercism.org/tracks/dart"
                    },
                    {
                        name: "LeetCode Dart问题",
                        url: "https://leetcode.com/tag/dart/"
                    },
                    {
                        name: "Flutter示例应用",
                        url: "https://flutter.github.io/samples/"
                    }
                ],
                projects: [
                    "开发一个Flutter移动应用",
                    "创建一个跨平台桌面应用",
                    "构建一个Web应用",
                    "开发一个简单的游戏",
                    "制作一个UI组件库"
                ],
                comparison: {
                    typeSystem: "静态类型(可选的)",
                    paradigm: "面向对象",
                    performance: "高性能(原生编译)",
                    learningCurve: "中等",
                    useCase: "跨平台移动应用, Web应用",
                    helloWorld: "void main() {\n  print('Hello, World!');\n}"
                }
            },
            {
                id: "ruby",
                name: "Ruby",
                type: ["web"],
                difficulty: "beginner",
                popularity: 60,
                description: "Ruby是一种动态、开源的编程语言，注重简洁和生产力。",
                info: "Ruby由Yukihiro Matsumoto于1995年发布，以其优雅的语法而闻名。Ruby on Rails框架极大地推动了Web开发的生产力。",
                image: "https://upload.wikimedia.org/wikipedia/commons/7/73/Ruby_logo.svg",
                official: "https://www.ruby-lang.org/",
                docs: "https://www.ruby-lang.org/en/documentation/",
                roadmap: {
                    beginner: [
                        "基本语法和数据类型",
                        "方法和块",
                        "类和模块",
                        "错误处理",
                        "常用标准库"
                    ],
                    intermediate: [
                        "元编程",
                        "Ruby on Rails基础",
                        "测试(RSpec)",
                        "Gem创建和发布",
                        "并发编程"
                    ],
                    advanced: [
                        "性能优化",
                        "C扩展开发",
                        "Ruby内部机制",
                        "框架深入(Rails, Sinatra)",
                        "设计模式应用"
                    ]
                },
                tutorials: [
                    {
                        title: "Ruby官方文档",
                        url: "https://www.ruby-lang.org/en/documentation/",
                        type: "文档"
                    },
                    {
                        title: "Ruby in Twenty Minutes",
                        url: "https://www.ruby-lang.org/en/documentation/quickstart/",
                        type: "教程"
                    },
                    {
                        title: "Learn Ruby the Hard Way",
                        url: "https://learnrubythehardway.org/book/",
                        type: "教程"
                    },
                    {
                        title: "Ruby中文文档",
                        url: "https://www.ruby-lang.org/zh_cn/documentation/"
                    }
                ],
                books: [
                    {
                        title: "The Well-Grounded Rubyist",
                        author: "David A. Black",
                        url: "https://www.manning.com/books/the-well-grounded-rubyist-third-edition",
                        free: false
                    },
                    {
                        title: "Eloquent Ruby",
                        author: "Russ Olsen",
                        url: "https://www.oreilly.com/library/view/eloquent-ruby/9780321700309/",
                        free: false
                    },
                    {
                        title: "Practical Object-Oriented Design in Ruby",
                        author: "Sandi Metz",
                        url: "https://www.oreilly.com/library/view/practical-object-oriented-design/9780132930871/",
                        free: false
                    }
                ],
                community: [
                    {
                        name: "Ruby官方论坛",
                        url: "https://www.ruby-lang.org/en/community/"
                    },
                    {
                        name: "Stack Overflow Ruby标签",
                        url: "https://stackoverflow.com/questions/tagged/ruby"
                    },
                    {
                        name: "Reddit r/ruby",
                        url: "https://www.reddit.com/r/ruby/"
                    },
                    {
                        name: "Ruby China",
                        url: "https://ruby-china.org/"
                    }
                ],
                practice: [
                    {
                        name: "Codewars Ruby问题",
                        url: "https://www.codewars.com/?language=ruby"
                    },
                    {
                        name: "Exercism Ruby学习路径",
                        url: "https://exercism.org/tracks/ruby"
                    },
                    {
                        name: "LeetCode Ruby问题",
                        url: "https://leetcode.com/tag/ruby/"
                    }
                ],
                projects: [
                    "开发一个简单的Web应用",
                    "创建一个命令行工具",
                    "构建一个API服务",
                    "开发一个爬虫",
                    "制作一个简单的游戏"
                ],
                comparison: {
                    typeSystem: "动态类型",
                    paradigm: "面向对象, 函数式",
                    performance: "中等",
                    learningCurve: "平缓",
                    useCase: "Web开发, 脚本, 自动化",
                    helloWorld: "puts 'Hello, World!'"
                }
            },
            {
                id: "php",
                name: "PHP",
                type: ["web"],
                difficulty: "beginner",
                popularity: 70,
                description: "PHP是一种广泛用于Web开发的服务器端脚本语言。",
                info: "PHP由Rasmus Lerdorf于1994年创建，现已成为最流行的Web开发语言之一。它特别适合与HTML集成，并支持多种数据库。",
                image: "https://upload.wikimedia.org/wikipedia/commons/2/27/PHP-logo.svg",
                official: "https://www.php.net/",
                docs: "https://www.php.net/docs.php",
                roadmap: {
                    beginner: [
                        "基本语法和数据类型",
                        "表单处理",
                        "会话和Cookie",
                        "文件操作",
                        "错误处理"
                    ],
                    intermediate: [
                        "面向对象编程",
                        "数据库访问(PDO, MySQLi)",
                        "Composer和包管理",
                        "安全最佳实践",
                        "框架基础(Laravel, Symfony)"
                    ],
                    advanced: [
                        "性能优化",
                        "扩展开发",
                        "API开发",
                        "测试(PHPUnit)",
                        "现代PHP特性(7.x, 8.x)"
                    ]
                },
                tutorials: [
                    {
                        title: "PHP官方文档",
                        url: "https://www.php.net/docs.php",
                        type: "文档"
                    },
                    {
                        title: "W3Schools PHP教程",
                        url: "https://www.w3schools.com/php/",
                        type: "交互式"
                    },
                    {
                        title: "PHP The Right Way",
                        url: "https://phptherightway.com/",
                        type: "最佳实践"
                    },
                    {
                        title: "PHP中文手册",
                        url: "https://www.php.net/manual/zh/"
                    }
                ],
                books: [
                    {
                        title: "Modern PHP",
                        author: "Josh Lockhart",
                        url: "https://www.oreilly.com/library/view/modern-php/9781491905173/",
                        free: false
                    },
                    {
                        title: "PHP Objects, Patterns, and Practice",
                        author: "Matt Zandstra",
                        url: "https://www.apress.com/gp/book/9781484219959",
                        free: false
                    },
                    {
                        title: "Laravel: Up & Running",
                        author: "Matt Stauffer",
                        url: "https://www.oreilly.com/library/view/laravel-up/9781492041207/",
                        free: false
                    }
                ],
                community: [
                    {
                        name: "PHP官方社区",
                        url: "https://www.php.net/support.php"
                    },
                    {
                        name: "Stack Overflow PHP标签",
                        url: "https://stackoverflow.com/questions/tagged/php"
                    },
                    {
                        name: "Reddit r/PHP",
                        url: "https://www.reddit.com/r/PHP/"
                    },
                    {
                        name: "PHPHub",
                        url: "https://phphub.org/"
                    }
                ],
                practice: [
                    {
                        name: "Codewars PHP问题",
                        url: "https://www.codewars.com/?language=php"
                    },
                    {
                        name: "Exercism PHP学习路径",
                        url: "https://exercism.org/tracks/php"
                    },
                    {
                        name: "LeetCode PHP问题",
                        url: "https://leetcode.com/tag/php/"
                    }
                ],
                projects: [
                    "开发一个博客系统",
                    "创建一个内容管理系统",
                    "构建一个电子商务网站",
                    "开发一个简单的API",
                    "制作一个用户认证系统"
                ],
                comparison: {
                    typeSystem: "动态类型",
                    paradigm: "多范式(过程式, 面向对象)",
                    performance: "中等",
                    learningCurve: "平缓",
                    useCase: "Web开发, 服务器端脚本",
                    helloWorld: "<?php\necho 'Hello, World!';\n?>"
                }
            }
        ];

        // 初始化页面
        document.addEventListener('DOMContentLoaded', function() {
            // 加载语言卡片
            renderLanguageCards();
            
            // 填充比较选择器
            populateComparisonSelectors();
            
            // 设置主题切换
            setupThemeToggle();
            
            // 设置搜索功能
            setupSearch();
            
            // 设置筛选功能
            setupFilters();
            
            // 设置比较按钮
            document.getElementById('compareButton').addEventListener('click', compareLanguages);
            
            // 设置模态框显示动画
            setupModalAnimation();
            
            // 设置卡片悬停效果
            setupCardHover();
        });

        // 渲染语言卡片
        function renderLanguageCards(filteredData = null) {
            const container = document.getElementById('languagesContainer');
            container.innerHTML = '';
            
            const data = filteredData || languagesData;
            
            data.forEach(lang => {
                const card = document.createElement('div');
                card.className = 'col-md-4 col-sm-6 animate__animated animate__fadeIn';
                card.innerHTML = `
                    <div class="card language-card" data-id="${lang.id}">
                        <div class="card-body">
                            <div class="d-flex align-items-center mb-3">
                                <img src="${lang.image}" alt="${lang.name} logo" class="language-icon me-3">
                                <h5 class="card-title mb-0">${lang.name}</h5>
                            </div>
                            <p class="card-text">${lang.description}</p>
                            <div class="d-flex justify-content-between align-items-center">
                                <span class="badge bg-${getTypeBadgeColor(lang.type[0])}">${getTypeName(lang.type[0])}</span>
                                <span class="badge bg-${getDifficultyBadgeColor(lang.difficulty)}">${getDifficultyName(lang.difficulty)}</span>
                            </div>
                        </div>
                        <div class="card-footer bg-transparent">
                            <button class="btn btn-sm btn-outline-primary w-100 view-details" data-id="${lang.id}">查看详情</button>
                        </div>
                    </div>
                `;
                container.appendChild(card);
            });
            
            // 添加查看详情事件
            document.querySelectorAll('.view-details').forEach(btn => {
                btn.addEventListener('click', function() {
                    const langId = this.getAttribute('data-id');
                    showLanguageDetails(langId);
                });
            });
        }

        // 显示语言详情
        function showLanguageDetails(langId) {
            const lang = languagesData.find(l => l.id === langId);
            if (!lang) return;
            
            // 设置基本信息
            document.getElementById('modalLanguageTitle').textContent = lang.name;
            document.getElementById('modalLanguageImage').src = lang.image;
            document.getElementById('modalLanguageInfo').textContent = lang.info;
            document.getElementById('modalLanguageDifficulty').textContent = getDifficultyName(lang.difficulty);
            document.getElementById('modalLanguageType').textContent = getTypeName(lang.type[0]);
            document.getElementById('modalLanguagePopularity').style.width = `${lang.popularity}%`;
            document.getElementById('modalLanguageOfficial').href = lang.official;
            document.getElementById('modalLanguageDocs').href = lang.docs;
            
            // 设置学习路线
            document.getElementById('modalBeginnerContent').innerHTML = lang.roadmap.beginner.map(item => `<p>• ${item}</p>`).join('');
            document.getElementById('modalIntermediateContent').innerHTML = lang.roadmap.intermediate.map(item => `<p>• ${item}</p>`).join('');
            document.getElementById('modalAdvancedContent').innerHTML = lang.roadmap.advanced.map(item => `<p>• ${item}</p>`).join('');
            
            // 设置教程资源
            document.getElementById('modalTutorials').innerHTML = lang.tutorials.map(tut => `
                <div class="resource-item bg-light smooth-transition">
                    <a href="${tut.url}" target="_blank">${tut.title}</a>
                    <span class="badge bg-secondary float-end">${tut.type}</span>
                </div>
            `).join('');
            
            // 设置书籍资源
            document.getElementById('modalBooks').innerHTML = lang.books.map(book => `
                <div class="resource-item bg-light mb-2 smooth-transition">
                    <a href="${book.url}" target="_blank">${book.title}</a> by ${book.author}
                    <span class="badge ${book.free ? 'bg-success' : 'bg-warning text-dark'} float-end">
                        ${book.free ? '免费' : '付费'}
                    </span>
                </div>
            `).join('');
            
            // 设置练习平台
            document.getElementById('modalPractice').innerHTML = lang.practice.map(prac => `
                <div class="resource-item bg-light smooth-transition">
                    <a href="${prac.url}" target="_blank">${prac.name}</a>
                </div>
            `).join('');
            
            // 设置社区链接
            document.getElementById('modalCommunity').innerHTML = lang.community.map(comm => `
                <div class="resource-item bg-light mb-2 smooth-transition">
                    <a href="${comm.url}" target="_blank">${comm.name}</a>
                </div>
            `).join('');
            
            // 设置项目创意
            document.getElementById('modalProjects').innerHTML = lang.projects.map((proj, idx) => `
                <div class="resource-item bg-light mb-2 smooth-transition">
                    <span class="me-2">${idx + 1}.</span> ${proj}
                </div>
            `).join('');
            
            // 显示模态框
            const modal = new bootstrap.Modal(document.getElementById('languageModal'));
            modal.show();
        }

        // 填充比较选择器
        function populateComparisonSelectors() {
            const select1 = document.getElementById('compareLanguage1');
            const select2 = document.getElementById('compareLanguage2');
            const select3 = document.getElementById('compareLanguage3');
            
            languagesData.forEach(lang => {
                const option = document.createElement('option');
                option.value = lang.id;
                option.textContent = lang.name;
                
                select1.appendChild(option.cloneNode(true));
                select2.appendChild(option.cloneNode(true));
                select3.appendChild(option.cloneNode(true));
            });
        }

        // 比较语言
        function compareLanguages() {
            const lang1Id = document.getElementById('compareLanguage1').value;
            const lang2Id = document.getElementById('compareLanguage2').value;
            const lang3Id = document.getElementById('compareLanguage3').value;
            
            if (!lang1Id || !lang2Id) {
                alert('请至少选择两种语言进行比较');
                return;
            }
            
            const lang1 = languagesData.find(l => l.id === lang1Id);
            const lang2 = languagesData.find(l => l.id === lang2Id);
            const lang3 = lang3Id ? languagesData.find(l => l.id === lang3Id) : null;
            
            // 更新表头
            document.getElementById('compareHeader1').textContent = lang1.name;
            document.getElementById('compareHeader2').textContent = lang2.name;
            
            if (lang3) {
                document.getElementById('compareHeader3').textContent = lang3.name;
                document.getElementById('compareHeader3').classList.remove('d-none');
                document.getElementById('typeSystem3').classList.remove('d-none');
                document.getElementById('paradigm3').classList.remove('d-none');
                document.getElementById('performance3').classList.remove('d-none');
                document.getElementById('learningCurve3').classList.remove('d-none');
                document.getElementById('useCase3').classList.remove('d-none');
                document.getElementById('helloWorld3').classList.remove('d-none');
            } else {
                document.getElementById('compareHeader3').classList.add('d-none');
                document.getElementById('typeSystem3').classList.add('d-none');
                document.getElementById('paradigm3').classList.add('d-none');
                document.getElementById('performance3').classList.add('d-none');
                document.getElementById('learningCurve3').classList.add('d-none');
                document.getElementById('useCase3').classList.add('d-none');
                document.getElementById('helloWorld3').classList.add('d-none');
            }
            
            // 填充比较数据
            document.getElementById('typeSystem1').textContent = lang1.comparison.typeSystem;
            document.getElementById('typeSystem2').textContent = lang2.comparison.typeSystem;
            if (lang3) document.getElementById('typeSystem3').textContent = lang3.comparison.typeSystem;
            
            document.getElementById('paradigm1').textContent = lang1.comparison.paradigm;
            document.getElementById('paradigm2').textContent = lang2.comparison.paradigm;
            if (lang3) document.getElementById('paradigm3').textContent = lang3.comparison.paradigm;
            
            document.getElementById('performance1').textContent = lang1.comparison.performance;
            document.getElementById('performance2').textContent = lang2.comparison.performance;
            if (lang3) document.getElementById('performance3').textContent = lang3.comparison.performance;
            
            document.getElementById('learningCurve1').textContent = lang1.comparison.learningCurve;
            document.getElementById('learningCurve2').textContent = lang2.comparison.learningCurve;
            if (lang3) document.getElementById('learningCurve3').textContent = lang3.comparison.learningCurve;
            
            document.getElementById('useCase1').textContent = lang1.comparison.useCase;
            document.getElementById('useCase2').textContent = lang2.comparison.useCase;
            if (lang3) document.getElementById('useCase3').textContent = lang3.comparison.useCase;
            
            document.getElementById('helloWorld1').textContent = lang1.comparison.helloWorld;
            document.getElementById('helloWorld2').textContent = lang2.comparison.helloWorld;
            if (lang3) document.getElementById('helloWorld3').textContent = lang3.comparison.helloWorld;
            
            // 显示表格
            document.getElementById('comparisonTable').classList.remove('d-none');
        }

        // 设置主题切换
        function setupThemeToggle() {
            const themeToggle = document.getElementById('themeToggle');
            const icon = themeToggle.querySelector('i');
            
            // 检查本地存储或系统偏好
            const savedTheme = localStorage.getItem('theme') || 
                             (window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light');
            
            if (savedTheme === 'dark') {
                document.body.classList.add('dark-mode');
                document.body.classList.remove('light-mode');
                icon.classList.replace('fa-moon', 'fa-sun');
            }
            
            themeToggle.addEventListener('click', function() {
                if (document.body.classList.contains('dark-mode')) {
                    document.body.classList.remove('dark-mode');
                    document.body.classList.add('light-mode');
                    icon.classList.replace('fa-sun', 'fa-moon');
                    localStorage.setItem('theme', 'light');
                } else {
                    document.body.classList.remove('light-mode');
                    document.body.classList.add('dark-mode');
                    icon.classList.replace('fa-moon', 'fa-sun');
                    localStorage.setItem('theme', 'dark');
                }
            });
        }

        // 设置搜索功能
        function setupSearch() {
            const searchInput = document.getElementById('searchInput');
            const searchButton = document.getElementById('searchButton');
            
            const performSearch = () => {
                const query = searchInput.value.toLowerCase();
                if (!query) {
                    renderLanguageCards();
                    return;
                }
                
                const filtered = languagesData.filter(lang => 
                    lang.name.toLowerCase().includes(query) || 
                    lang.description.toLowerCase().includes(query) ||
                    lang.type.some(t => getTypeName(t).toLowerCase().includes(query))
                );
                
                renderLanguageCards(filtered);
            };
            
            searchButton.addEventListener('click', performSearch);
            searchInput.addEventListener('keyup', function(e) {
                if (e.key === 'Enter') performSearch();
            });
        }

        // 设置筛选功能
        function setupFilters() {
            const typeFilter = document.getElementById('languageTypeFilter');
            const difficultyFilter = document.getElementById('difficultyFilter');
            
            const applyFilters = () => {
                const type = typeFilter.value;
                const difficulty = difficultyFilter.value;
                
                const filtered = languagesData.filter(lang => {
                    const typeMatch = type === 'all' || lang.type.includes(type);
                    const difficultyMatch = difficulty === 'all' || lang.difficulty === difficulty;
                    return typeMatch && difficultyMatch;
                });
                
                renderLanguageCards(filtered);
            };
            
            typeFilter.addEventListener('change', applyFilters);
            difficultyFilter.addEventListener('change', applyFilters);
        }

        // 设置模态框动画
        function setupModalAnimation() {
            const modal = document.getElementById('languageModal');
            modal.addEventListener('show.bs.modal', function() {
                this.querySelector('.modal-content').classList.add('animate__animated', 'animate__fadeInUp');
            });
            
            modal.addEventListener('hidden.bs.modal', function() {
                this.querySelector('.modal-content').classList.remove('animate__animated', 'animate__fadeInUp');
            });
        }

        // 设置卡片悬停效果
        function setupCardHover() {
            document.addEventListener('mousemove', function(e) {
                const cards = document.querySelectorAll('.language-card');
                cards.forEach(card => {
                    const rect = card.getBoundingClientRect();
                    const x = e.clientX - rect.left;
                    const y = e.clientY - rect.top;
                    
                    card.style.setProperty('--mouse-x', `${x}px`);
                    card.style.setProperty('--mouse-y', `${y}px`);
                });
            });
        }

        // 辅助函数
        function getTypeName(type) {
            const types = {
                'web': 'Web开发',
                'mobile': '移动开发',
                'desktop': '桌面应用',
                'data': '数据科学',
                'system': '系统编程',
                'game': '游戏开发'
            };
            return types[type] || type;
        }

        function getTypeBadgeColor(type) {
            const colors = {
                'web': 'primary',
                'mobile': 'success',
                'desktop': 'info',
                'data': 'warning',
                'system': 'danger',
                'game': 'dark'
            };
            return colors[type] || 'secondary';
        }

        function getDifficultyName(difficulty) {
            const names = {
                'beginner': '初级',
                'intermediate': '中级',
                'advanced': '高级'
            };
            return names[difficulty] || difficulty;
        }

        function getDifficultyBadgeColor(difficulty) {
            const colors = {
                'beginner': 'success',
                'intermediate': 'warning',
                'advanced': 'danger'
            };
            return colors[difficulty] || 'secondary';
        }
    </script>
</body>
</html>
