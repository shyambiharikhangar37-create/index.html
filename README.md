<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>बुंदेली बौछार BUNDELI BAUCHHAR</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        
        /* Scroll Snap Configuration for Center Alignment */
        html {
            scroll-snap-type: y mandatory;
            scroll-behavior: smooth;
            scroll-padding-top: 140px;    /* Header + Categories height adjustment */
            scroll-padding-bottom: 80px;  /* Bottom nav height adjustment */
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #0f1410;
            color: #fff;
            min-height: 100vh;
        }
        
        .header {
            background: linear-gradient(135deg, #2e7d32, #c62828, #f9a825);
            padding: 20px;
            text-align: center;
            box-shadow: 0 4px 6px rgba(0,0,0,0.5);
            position: sticky;
            top: 0;
            z-index: 100;
        }
        
        .header h1 { font-size: 26px; font-weight: bold; letter-spacing: 1px; }
        .header p { font-size: 13px; margin-top: 5px; opacity: 0.95; }
        
        .categories {
            display: flex;
            overflow-x: auto;
            padding: 15px;
            gap: 10px;
            background: #1a241a;
            position: sticky;
            top: 76px;
            z-index: 90;
        }
        
        .category-btn {
            background: #2a3a2a;
            color: #fff;
            border: none;
            padding: 10px 20px;
            border-radius: 20px;
            cursor: pointer;
            white-space: nowrap;
            transition: all 0.3s;
        }
        
        .category-btn.active { background: #c62828; }
        .category-btn:hover { background: #f9a825; color: #000; }
        
        .video-list { padding: 15px; }
        
        .video-card {
            background: #1a241a;
            border-radius: 12px;
            margin-bottom: 20px;
            overflow: visible;
            box-shadow: 0 2px 10px rgba(0,0,0,0.5);
            border: 1px solid #2a3a2a;
            position: relative;
            z-index: 1;
            /* Scroll Snap Properties */
            scroll-snap-align: center;
            scroll-snap-stop: always;
        }
        
        .video-wrapper {
            position: relative;
            padding-bottom: 56.25%;
            height: 0;
            background: #000;
            overflow: visible;
            z-index: 1000;
        }
        
        .youtube-player-div {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1000;
        }

        /* ROBUST FULLSCREEN CSS */
        .video-wrapper:fullscreen,
        .video-wrapper:-webkit-full-screen,
        .video-wrapper:-moz-full-screen,
        .video-wrapper:-ms-fullscreen {
            width: 100vw !important;
            height: 100vh !important;
            height: 100dvh !important;
            max-width: 100vw !important;
            max-height: 100vh !important;
            max-height: 100dvh !important;
            padding-bottom: 0 !important;
            background: #000 !important;
            display: flex !important;
            align-items: center !important;
            justify-content: center !important;
            position: fixed !important;
            top: 0 !important;
            left: 0 !important;
            right: 0 !important;
            bottom: 0 !important;
            z-index: 2147483647 !important;
            margin: 0 !important;
            border: none !important;
            overflow: hidden !important;
        }
        
        .video-wrapper:fullscreen .youtube-player-div,
        .video-wrapper:-webkit-full-screen .youtube-player-div,
        .video-wrapper:-moz-full-screen .youtube-player-div,
        .video-wrapper:-ms-fullscreen .youtube-player-div,
        .video-wrapper:fullscreen iframe,
        .video-wrapper:-webkit-full-screen iframe,
        .video-wrapper:-moz-full-screen iframe,
        .video-wrapper:-ms-fullscreen iframe {
            width: 100% !important;
            height: 100% !important;
            min-width: 100% !important;
            min-height: 100% !important;
            position: absolute !important;
            top: 0 !important;
            left: 0 !important;
            right: 0 !important;
            bottom: 0 !important;
            border: none !important;
            z-index: 2147483647 !important;
        }

        .fullscreen-controls {
            position: absolute;
            top: 15px;
            right: 15px;
            z-index: 2147483647;
            display: none;
        }
        
        .video-wrapper:fullscreen .fullscreen-controls,
        .video-wrapper:-webkit-full-screen .fullscreen-controls,
        .video-wrapper:-moz-full-screen .fullscreen-controls,
        .video-wrapper:-ms-fullscreen .fullscreen-controls {
            display: flex !important;
            position: absolute !important;
            top: 20px !important;
            right: 20px !important;
            z-index: 2147483647 !important;
        }
        
        .close-fullscreen {
            background: rgba(0,0,0,0.7);
            color: #fff;
            border: 2px solid #fff;
            width: 44px;
            height: 44px;
            border-radius: 50%;
            font-size: 24px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            pointer-events: auto !important;
            box-shadow: 0 2px 8px rgba(0,0,0,0.5);
            transition: transform 0.2s;
            z-index: 2147483647 !important;
        }
        
        .close-fullscreen:active {
            background: rgba(255,255,255,0.2);
            transform: scale(0.95);
        }
        
        /* Compact action buttons - directly below video */
        .video-actions-compact {
            display: flex;
            justify-content: space-around;
            align-items: center;
            padding: 10px 15px;
            background: #1a241a;
            border-bottom: 1px solid #2a3a2a;
            position: relative;
            z-index: 10;
        }
        
        .action-btn-compact {
            background: none;
            border: none;
            color: #ccc;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 4px;
            cursor: pointer;
            font-size: 12px;
            padding: 5px 10px;
            transition: all 0.2s;
            position: relative;
            z-index: 10;
        }
        
        .action-btn-compact:hover { color: #f9a825; }
        .action-btn-compact.liked { color: #c62828; }
        .action-btn-compact .icon { font-size: 22px; }
        .action-btn-compact .label { font-size: 11px; }
        
        .video-info { 
            padding: 12px 15px;
            position: relative;
            z-index: 10;
        }
        .video-title { 
            font-size: 16px; 
            font-weight: bold; 
            margin-bottom: 5px; 
            color: #f9a825; 
        }
        .video-desc { 
            font-size: 13px; 
            color: #aaa; 
        }
        
        /* Ad container styles */
        .ad-container {
            background: #0f1410;
            padding: 12px 15px;
            border-top: 1px solid #2a3a2a;
            border-bottom: 1px solid #2a3a2a;
            position: relative;
            z-index: 10;
        }
        
        .ad-label {
            font-size: 10px;
            color: #555;
            text-align: center;
            margin-bottom: 5px;
        }
        
        .ad-placeholder {
            width: 100%;
            height: 90px;
            background: linear-gradient(135deg, #1a241a, #2a3a2a);
            border: 2px dashed #3a4a3a;
            border-radius: 8px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #666;
            font-size: 13px;
            text-align: center;
        }
        
        .comment-section {
            padding: 12px 15px;
            background: #0f1410;
            position: relative;
            z-index: 10;
        }
        
        .comment-section h4 { color: #f9a825; font-size: 13px; margin-bottom: 8px; }
        
        .comment-input {
            display: flex;
            gap: 8px;
            margin-bottom: 10px;
        }
        
        .comment-input input {
            flex: 1;
            background: #1a241a;
            color: #fff;
            border: 1px solid #2a3a2a;
            border-radius: 20px;
            padding: 8px 14px;
            font-size: 13px;
            outline: none;
        }
        
        .comment-input button {
            background: #2e7d32;
            color: #fff;
            border: none;
            padding: 8px 14px;
            border-radius: 20px;
            cursor: pointer;
            font-size: 13px;
        }
        
        .comments-list {
            max-height: 200px;
            overflow-y: auto;
        }
        
        .comment-item {
            background: #1a241a;
            padding: 8px 12px;
            border-radius: 8px;
            margin-bottom: 6px;
            font-size: 13px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .comment-item .del {
            color: #c62828;
            cursor: pointer;
            background: none;
            border: none;
            font-size: 14px;
        }
        
        .comment-item .name { color: #f9a825; font-weight: bold; }
        
        .modal {
            display: none;
            position: fixed;
            inset: 0;
            background: rgba(0,0,0,0.8);
            z-index: 2000;
            justify-content: center;
            align-items: center;
        }
        
        .modal.show { display: flex; }
        
        .modal-content {
            background: #1a241a;
            border-radius: 12px;
            padding: 20px;
            width: 90%;
            max-width: 350px;
        }
        
        .modal-content h3 { color: #f9a825; margin-bottom: 15px; text-align: center; }
        
        .share-options {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 12px;
            margin-bottom: 15px;
        }
        
        .share-btn {
            background: #2a3a2a;
            border: none;
            color: #fff;
            padding: 14px 8px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 13px;
            text-align: center;
        }
        
        .share-btn:hover { background: #3a4a3a; }
        .share-btn .icon { font-size: 28px; display: block; margin-bottom: 4px; }
        
        .close-modal {
            width: 100%;
            background: #c62828;
            color: #fff;
            border: none;
            padding: 10px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 14px;
        }
        
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 0;
            right: 0;
            background: #1a241a;
            display: flex;
            justify-content: space-around;
            padding: 12px 0;
            box-shadow: 0 -2px 10px rgba(0,0,0,0.5);
            z-index: 1000;
            border-top: 2px solid #2e7d32;
        }
        
        .nav-item {
            text-align: center;
            color: #aaa;
            cursor: pointer;
            transition: color 0.3s;
        }
        .nav-item.active { color: #f9a825; }
        .nav-item span { display: block; font-size: 11px; margin-top: 4px; }
        
        .content { padding-bottom: 80px; }
        
        .categories::-webkit-scrollbar { display: none; }
        .categories { -ms-overflow-style: none; scrollbar-width: none; }
        
        .toast {
            position: fixed;
            bottom: 100px;
            left: 50%;
            transform: translateX(-50%);
            background: #2e7d32;
            color: #fff;
            padding: 10px 20px;
            border-radius: 20px;
            z-index: 3000;
            opacity: 0;
            transition: opacity 0.3s;
            pointer-events: none;
        }
        
        .toast.show { opacity: 1; }
        
        /* Hide UI elements completely during fullscreen */
        body.fullscreen-mode .header,
        body.fullscreen-mode .categories,
        body.fullscreen-mode .bottom-nav {
            display: none !important;
        }
        body.fullscreen-mode .content {
            padding-bottom: 0 !important;
            height: 100vh !important;
            height: 100dvh !important;
            overflow: hidden !important;
        }

        /* Landscape Mode: Show ONLY video list, hide everything else */
        @media (orientation: landscape) {
            .header,
            .categories,
            .bottom-nav,
            .video-actions-compact,
            .video-info,
            .ad-container,
            .comment-section {
                display: none !important;
            }
            
            body {
                background: #000 !important;
                padding: 0 !important;
                margin: 0 !important;
            }
            
            .content {
                padding: 0 !important;
                padding-bottom: 0 !important;
                height: auto !important;
                overflow: visible !important;
            }
            
            .video-list {
                padding: 0 !important;
                height: auto !important;
                overflow-y: visible !important;
                display: flex !important;
                flex-direction: column !important;
                gap: 0 !important;
            }
            
            .video-card {
                margin: 0 !important;
                border-radius: 0 !important;
                border: none !important;
                border-bottom: 2px solid #2a3a2a !important;
                height: auto !important;
                min-height: auto !important;
                max-height: none !important;
                background: #000 !important;
                display: flex !important;
                flex-direction: column !important;
                flex-shrink: 0 !important;
                width: 100% !important;
                /* Ensure snap works in landscape too */
                scroll-snap-align: center !important;
            }
            
            .video-wrapper {
                width: 100% !important;
                height: auto !important;
                padding-bottom: 56.25% !important;
                position: relative !important;
                background: #000 !important;
            }
            
            .youtube-player-div, 
            .youtube-player-div iframe {
                width: 100% !important;
                height: 100% !important;
                position: absolute !important;
                top: 0 !important;
                left: 0 !important;
                right: 0 !important;
                bottom: 0 !important;
            }
        }
    </style>
</head>
<body>
    <div class="header" id="mainHeader">
        <h1>🌾 बुंदेली बौछार </h1>
        <p>BUNDELI BAUCHHAR (bundelkhand)</p>
        <p>बुंदेलखंड की माटी की महक - गीत, नाटक, कहानियाँ</p>
    </div>
    
    <div class="content">
        <div class="categories" id="mainCategories">
            <button class="category-btn active" onclick="filterCategory('all', this)">सभी</button>
            <button class="category-btn" onclick="filterCategory('song', this)">लोकगीत</button>
            <button class="category-btn" onclick="filterCategory('drama', this)">नाटक</button>
            <button class="category-btn" onclick="filterCategory('comedy', this)">हास्य</button>
            <button class="category-btn" onclick="filterCategory('story', this)">कहानी</button>
            <button class="category-btn" onclick="filterCategory('culture', this)">संस्कृति</button>
        </div>
        
        <div class="video-list" id="videoList"></div>
    </div>
    
    <div class="bottom-nav" id="mainNav">
        <div class="nav-item active" onclick="showPage('home', this)">🏠<span>होम</span></div>
        <div class="nav-item" onclick="showPage('search', this)">🔍<span>खोजें</span></div>
        <div class="nav-item" onclick="showPage('upload', this)">➕<span>अपलोड</span></div>
        <div class="nav-item" onclick="showPage('profile', this)">👤<span>प्रोफ़ाइल</span></div>
    </div>
    
    <!-- Share Modal -->
    <div class="modal" id="shareModal">
        <div class="modal-content">
            <h3>📤 शेयर करें</h3>
            <div class="share-options">
                <button class="share-btn" onclick="shareVia('whatsapp')"><span class="icon">💬</span>WhatsApp</button>
                <button class="share-btn" onclick="shareVia('facebook')"><span class="icon">📘</span>Facebook</button>
                <button class="share-btn" onclick="shareVia('twitter')"><span class="icon">🐦</span>Twitter</button>
                <button class="share-btn" onclick="shareVia('telegram')"><span class="icon">✈️</span>Telegram</button>
                <button class="share-btn" onclick="shareVia('copy')"><span class="icon">🔗</span>Copy Link</button>
                <button class="share-btn" onclick="shareVia('more')"><span class="icon">⋯</span>और</button>
            </div>
            <button class="close-modal" onclick="closeModal()">बंद करें</button>
        </div>
    </div>
    
    <!-- Download Modal -->
    <div class="modal" id="downloadModal">
        <div class="modal-content">
            <h3>⬇️ डाउनलोड करें</h3>
            <p style="color: #aaa; font-size: 13px; margin-bottom: 15px; text-align: center;">
                वीडियो डाउनलोड करने के लिए लिंक कॉपी करें:
            </p>
            <div style="background: #0f1410; padding: 10px; border-radius: 8px; word-break: break-all; font-size: 12px; margin-bottom: 12px;" id="downloadLink"></div>
            <button class="share-btn" style="width: 100%; margin-bottom: 10px;" onclick="copyDownloadLink()">📋 लिंक कॉपी करें</button>
            <button class="share-btn" style="width: 100%; margin-bottom: 10px; background: #2e7d32;" onclick="openDownloader()">🔽 डाउनलोडर खोलें</button>
            <button class="close-modal" onclick="closeDownloadModal()">बंद करें</button>
        </div>
    </div>
    
    <div class="toast" id="toast"></div>

    <script>
        const videos = [
            { id: 1, title: "हरदौल की लीला - बुंदेली नाटक", desc: "बुंदेलखंड की प्रसिद्ध लोक कथा", category: "drama", youtubeId: "4NpfAs5_vLs" },
            { id: 2, title: "बुंदेली लोकगीत - रैया", desc: "माटी की खुशबू भरे गीत", category: "song", youtubeId: "o0bkp9zwNk4" },
            { id: 3, title: "बुंदेली हास्य कवि सम्मेलन", desc: "हँसी-मज़ाक का मेला", category: "comedy", youtubeId: "dQw4w9WgXcQ" },
            { id: 4, title: "छाँद कौरी की कहानी", desc: "बुंदेलखंड की प्रेम कथा", category: "story", youtubeId: "juKd26qkWAo" },
            { id: 5, title: "दीवारियाँ नाटक - बुंदेली", desc: "समाज पर व्यंग्य", category: "drama", youtubeId: "kqtD5dpn9C8" },
            { id: 6, title: "बुंदेली संस्कृति और त्योहार", desc: "हमारी पहचान, हमारी धरोहर", category: "culture", youtubeId: "wNDGgL73ihY" }
        ];
        
        let currentShareId = null;
        let currentDownloadId = null;
        let observer = null;
        let visibleVideoId = null;
        
        // YouTube Player API Variables
        let ytPlayers = {};
        let isYtReady = false;

        window.onYouTubeIframeAPIReady = function() {
            isYtReady = true;
            initializePlayers();
        };

        function initializePlayers() {
            document.querySelectorAll('.youtube-player-div').forEach(div => {
                const videoId = div.id.replace('player_', '');
                const video = videos.find(v => v.id == videoId);
                if (video && !ytPlayers[video.id]) {
                    ytPlayers[video.id] = new YT.Player(div.id, {
                        videoId: video.youtubeId,
                        playerVars: {
                            'autoplay': 0,
                            'controls': 1,
                            'rel': 0,
                            'playsinline': 1,
                            'fs': 1
                        }
                    });
                }
            });
        }

        var tag = document.createElement('script');
        tag.src = "https://www.youtube.com/iframe_api";
        var firstScriptTag = document.getElementsByTagName('script')[0];
        firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
        
        function showToast(msg) {
            const toast = document.getElementById('toast');
            toast.textContent = msg;
            toast.classList.add('show');
            setTimeout(() => toast.classList.remove('show'), 2000);
        }
        
        function loadVideos(category = 'all') {
            Object.keys(ytPlayers).forEach(key => {
                if (ytPlayers[key] && typeof ytPlayers[key].destroy === 'function') {
                    ytPlayers[key].destroy();
                }
            });
            ytPlayers = {};
            visibleVideoId = null;

            const videoList = document.getElementById('videoList');
            videoList.innerHTML = '';
            
            const filtered = category === 'all' ? videos : videos.filter(v => v.category === category);
            
            filtered.forEach(video => {
                const likeCount = parseInt(localStorage.getItem(`like_${video.id}`) || '0');
                const isLiked = localStorage.getItem(`liked_${video.id}`) === 'true';
                const comments = JSON.parse(localStorage.getItem(`comments_${video.id}`) || '[]');
                
                const card = document.createElement('div');
                card.className = 'video-card';
                card.innerHTML = `
                    <div class="video-wrapper" id="wrapper_${video.id}">
                        <div class="fullscreen-controls">
                            <button class="close-fullscreen" onclick="toggleFullscreen(${video.id})" title="फुल स्क्रीन बंद करें (ESC)">✕</button>
                        </div>
                        <div id="player_${video.id}" class="youtube-player-div"></div>
                    </div>
                    
                    <!-- Compact action buttons directly below video -->
                    <div class="video-actions-compact">
                        <button class="action-btn-compact ${isLiked ? 'liked' : ''}" onclick="toggleLike(${video.id}, this, ${likeCount})">
                            <span class="icon">${isLiked ? '❤️' : '🤍'}</span>
                            <span class="label">${likeCount}</span>
                        </button>
                        <button class="action-btn-compact" onclick="toggleComments(${video.id})">
                            <span class="icon">💬</span>
                            <span class="label">${comments.length}</span>
                        </button>
                        <button class="action-btn-compact" onclick="openShare(${video.id}, '${video.title.replace(/'/g, "\\'")}')">
                            <span class="icon">📤</span>
                            <span class="label">शेयर</span>
                        </button>
                        <button class="action-btn-compact" onclick="openDownload(${video.id}, '${video.youtubeId}')">
                            <span class="icon">⬇️</span>
                            <span class="label">डाउनलोड</span>
                        </button>
                        <button class="action-btn-compact" onclick="toggleFullscreen(${video.id})">
                            <span class="icon">⛶</span>
                            <span class="label">फुल स्क्रीन</span>
                        </button>
                    </div>
                    
                    <!-- Video info -->
                    <div class="video-info">
                        <div class="video-title">${video.title}</div>
                        <div class="video-desc">${video.desc}</div>
                    </div>
                    
                    <!-- Ad container -->
                    <div class="ad-container">
                        <div class="ad-label">विज्ञापन</div>
                        <div class="ad-placeholder">
                            यहाँ आपका विज्ञापन दिखेगा<br>
                            (Ad Space - 300x100)
                        </div>
                    </div>
                    
                    <div class="comment-section" id="comments_${video.id}" style="display:none;">
                        <h4>💭 टिप्पणियाँ (${comments.length})</h4>
                        <div class="comment-input">
                            <input type="text" id="cinput_${video.id}" placeholder="अपनी राय लिखें...">
                            <button onclick="addComment(${video.id})">भेजें</button>
                        </div>
                        <div class="comments-list" id="clist_${video.id}">
                            ${comments.map((c, i) => `
                                <div class="comment-item">
                                    <div><span class="name">${c.name}:</span> ${c.text}</div>
                                    <button class="del" onclick="deleteComment(${video.id}, ${i})">✕</button>
                                </div>
                            `).join('')}
                        </div>
                    </div>
                `;
                videoList.appendChild(card);
            });
            
            if (isYtReady) {
                setTimeout(initializePlayers, 100);
            }
            
            setTimeout(setupIntersectionObserver, 500);
        }
        
        function toggleFullscreen(videoId) {
            const wrapper = document.getElementById(`wrapper_${videoId}`);
            const player = ytPlayers[videoId];
            const isCurrentlyFullscreen = document.fullscreenElement || document.webkitFullscreenElement || document.mozFullScreenElement || document.msFullscreenElement;
            
            if (!isCurrentlyFullscreen) {
                let promise = null;
                if (wrapper.requestFullscreen) {
                    promise = wrapper.requestFullscreen();
                } else if (wrapper.webkitRequestFullscreen) {
                    promise = wrapper.webkitRequestFullscreen();
                } else if (wrapper.mozRequestFullScreen) {
                    promise = wrapper.mozRequestFullScreen();
                } else if (wrapper.msRequestFullscreen) {
                    promise = wrapper.msRequestFullscreen();
                }
                
                if (promise) {
                    promise.catch(err => {
                        console.warn("Fullscreen request failed:", err);
                    });
                }
                
                pauseAllVideos();
                visibleVideoId = videoId;
                
                setTimeout(() => {
                    if (player && typeof player.playVideo === 'function') {
                        player.playVideo();
                    }
                }, 600);
            } else {
                if (document.exitFullscreen) {
                    document.exitFullscreen();
                } else if (document.webkitExitFullscreen) {
                    document.webkitExitFullscreen();
                } else if (document.mozCancelFullScreen) {
                    document.mozCancelFullScreen();
                } else if (document.msExitFullscreen) {
                    document.msExitFullscreen();
                }
            }
        }
        
        function handleFullscreenChange() {
            const isFullscreen = document.fullscreenElement || document.webkitFullscreenElement || document.mozFullScreenElement || document.msFullscreenElement;
            
            if (!isFullscreen) {
                document.body.classList.remove('fullscreen-mode');
                if (visibleVideoId && ytPlayers[visibleVideoId] && typeof ytPlayers[visibleVideoId].pauseVideo === 'function') {
                    ytPlayers[visibleVideoId].pauseVideo();
                }
                visibleVideoId = null;
            } else {
                document.body.classList.add('fullscreen-mode');
            }
        }
        
        document.addEventListener('fullscreenchange', handleFullscreenChange);
        document.addEventListener('webkitfullscreenchange', handleFullscreenChange);
        document.addEventListener('mozfullscreenchange', handleFullscreenChange);
        document.addEventListener('MSFullscreenChange', handleFullscreenChange);
        
        function setupIntersectionObserver() {
            if (observer) observer.disconnect();
            
            observer = new IntersectionObserver((entries) => {
                if (document.fullscreenElement || document.webkitFullscreenElement || document.mozFullScreenElement || document.msFullscreenElement) return;
                
                entries.forEach(entry => {
                    const videoId = entry.target.getAttribute('data-video-id');
                    const player = ytPlayers[videoId];
                    
                    if (entry.isIntersecting && entry.intersectionRatio > 0.6) {
                        if (player && typeof player.playVideo === 'function' && visibleVideoId !== videoId) {
                            pauseAllVideos();
                            player.playVideo();
                            visibleVideoId = videoId;
                        }
                    } else {
                        if (player && typeof player.pauseVideo === 'function' && visibleVideoId === videoId) {
                            player.pauseVideo();
                        }
                    }
                });
            }, { 
                threshold: [0.6, 0.8, 1.0],
                rootMargin: '0px'
            });
            
            document.querySelectorAll('.video-wrapper').forEach(wrapper => {
                const videoId = wrapper.id.replace('wrapper_', '');
                wrapper.setAttribute('data-video-id', videoId);
                observer.observe(wrapper);
            });
        }
        
        function pauseAllVideos() {
            Object.values(ytPlayers).forEach(player => {
                if (player && typeof player.pauseVideo === 'function') {
                    player.pauseVideo();
                }
            });
            visibleVideoId = null;
        }
        
        function toggleLike(videoId, btn, currentCount) {
            const isLiked = localStorage.getItem(`liked_${videoId}`) === 'true';
            let count = currentCount;
            
            if (isLiked) {
                localStorage.removeItem(`liked_${videoId}`);
                count--;
                btn.classList.remove('liked');
                btn.querySelector('.icon').textContent = '🤍';
            } else {
                localStorage.setItem(`liked_${videoId}`, 'true');
                count++;
                btn.classList.add('liked');
                btn.querySelector('.icon').textContent = '❤️';
                showToast('❤️ पसंद किया!');
            }
            localStorage.setItem(`like_${videoId}`, count);
            btn.querySelector('.label').textContent = count;
        }
        
        function toggleComments(videoId) {
            const section = document.getElementById(`comments_${videoId}`);
            section.style.display = section.style.display === 'none' ? 'block' : 'none';
        }
        
        function addComment(videoId) {
            const input = document.getElementById(`cinput_${videoId}`);
            const text = input.value.trim();
            if (!text) return;
            
            const comments = JSON.parse(localStorage.getItem(`comments_${videoId}`) || '[]');
            const name = localStorage.getItem('userName') || 'अतिथि';
            comments.unshift({ name, text, time: Date.now() });
            localStorage.setItem(`comments_${videoId}`, JSON.stringify(comments));
            input.value = '';
            showToast('✅ टिप्पणी जोड़ी गई!');
            
            const activeBtn = document.querySelector('.category-btn.active');
            const category = activeBtn.textContent === 'सभी' ? 'all' : activeBtn.getAttribute('onclick').match(/'([^']+)'/)[1];
            loadVideos(category);
        }
        
        function deleteComment(videoId, index) {
            const comments = JSON.parse(localStorage.getItem(`comments_${videoId}`) || '[]');
            comments.splice(index, 1);
            localStorage.setItem(`comments_${videoId}`, JSON.stringify(comments));
            
            const activeBtn = document.querySelector('.category-btn.active');
            const category = activeBtn.textContent === 'सभी' ? 'all' : activeBtn.getAttribute('onclick').match(/'([^']+)'/)[1];
            loadVideos(category);
            showToast('🗑️ टिप्पणी हटाई गई');
        }
        
        function openShare(videoId, title) {
            currentShareId = videoId;
            const video = videos.find(v => v.id === videoId);
            window.currentShareUrl = `https://youtu.be/${video.youtubeId}`;
            window.currentShareText = `${title} - बुंदेली बौछार में देखें`;
            document.getElementById('shareModal').classList.add('show');
        }
        
        function shareVia(platform) {
            const url = encodeURIComponent(window.currentShareUrl);
            const text = encodeURIComponent(window.currentShareText);
            let shareUrl = '';
            
            switch(platform) {
                case 'whatsapp': shareUrl = `https://wa.me/?text=${text}%20${url}`; break;
                case 'facebook': shareUrl = `https://www.facebook.com/sharer/sharer.php?u=${url}`; break;
                case 'twitter': shareUrl = `https://twitter.com/intent/tweet?text=${text}&url=${url}`; break;
                case 'telegram': shareUrl = `https://t.me/share/url?url=${url}&text=${text}`; break;
                case 'copy':
                    navigator.clipboard.writeText(window.currentShareUrl).then(() => showToast('🔗 लिंक कॉपी हो गया!'));
                    closeModal(); return;
                case 'more':
                    if (navigator.share) {
                        navigator.share({ title: window.currentShareText, url: window.currentShareUrl });
                    } else {
                        showToast('⚠️ शेयर उपलब्ध नहीं');
                    }
                    closeModal(); return;
            }
            window.open(shareUrl, '_blank');
            closeModal();
        }
        
        function closeModal() { document.getElementById('shareModal').classList.remove('show'); }
        
        function openDownload(videoId, youtubeId) {
            currentDownloadId = videoId;
            const url = `https://www.youtube.com/watch?v=${youtubeId}`;
            document.getElementById('downloadLink').textContent = url;
            window.currentDownloadUrl = url;
            document.getElementById('downloadModal').classList.add('show');
        }
        
        function copyDownloadLink() {
            navigator.clipboard.writeText(window.currentDownloadUrl).then(() => showToast('📋 लिंक कॉपी हो गया!'));
        }
        
        function openDownloader() {
            window.open(`https://www.y2mate.com/youtube/${window.currentDownloadUrl.split('v=')[1]}`, '_blank');
            closeDownloadModal();
        }
        
        function closeDownloadModal() { document.getElementById('downloadModal').classList.remove('show'); }
        
        function filterCategory(category, btn) {
            document.querySelectorAll('.category-btn').forEach(b => b.classList.remove('active'));
            btn.classList.add('active');
            loadVideos(category);
        }
        
        function showPage(page, navItem) {
            document.querySelectorAll('.nav-item').forEach(i => i.classList.remove('active'));
            navItem.classList.add('active');
            
            if (page === 'home') loadVideos();
            else if (page === 'search') showToast('🔍 खोज सुविधा जल्द आ रही है!');
            else if (page === 'upload') {
                const name = prompt('अपना नाम दर्ज करें:');
                if (name) { localStorage.setItem('userName', name); showToast(`स्वागत है ${name} जी! 🌾`); }
            } else if (page === 'profile') {
                const name = localStorage.getItem('userName') || 'अतिथि';
                alert(`👤 प्रोफ़ाइल\n\nनाम: ${name}\n\n🌾 बुंदेली बौछार में आपका स्वागत है!`);
            }
        }
        
        // Handle orientation change
        window.addEventListener('orientationchange', function() {
            setTimeout(() => {
                setupIntersectionObserver();
            }, 300);
        });
        
        if (!localStorage.getItem('userName')) localStorage.setItem('userName', 'बुंदेली-प्रेमी');
        loadVideos();
    </script>
</body>
</html>
