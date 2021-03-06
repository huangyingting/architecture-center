---
title: Scalable Umbraco CMS web app
titleSuffix: Azure Solution Ideas
author: adamboeglin
ms.date: 12/16/2019
description: Medium Umbraco CMS web app configured to scale and optimal for high-traffic sites. It uses two web apps, one for your front-end app and the other for your back-office app, deployed in a single region with autoscaling enabled.
ms.custom: acom-architecture, web-apps, app-dev, is-deployable, 'https://azure.microsoft.com/solutions/architecture/medium-umbraco-web-app/'
ms.service: architecture-center
ms.subservice: solution-idea
---
# Scalable Umbraco CMS web app

[!INCLUDE [header_file](../header.md)]

Medium Umbraco CMS web app configured to scale and optimal for high-traffic sites. It uses two web apps, one for your front-end app and the other for your back-office app, deployed in a single region with autoscaling enabled.

This solution is built on the Azure managed services: [Azure SQL Database](https://azure.microsoft.com/services/sql-database/), [Storage Accounts](https://azure.microsoft.com/services/storage/), Application Insights and [Azure Cache for Redis](https://azure.microsoft.com/services/cache/). These services run in a high-availability environment, patched and supported, allowing you to focus on your solution instead of the environment they run in.

## Architecture

<svg class="architecture-diagram" aria-labelledby="medium-umbraco-web-app" height="403.089" viewbox="0 0 655.575 403.089"  xmlns="http://www.w3.org/2000/svg">
    <path fill="none" stroke="#B5B5B5" stroke-miterlimit="10" stroke-width="1.643" d="M96.803 144.728h88.827"/>
    <path fill="#B5B5B5" d="M184.432 148.824l7.092-4.096-7.092-4.095z"/>
    <path fill="none" stroke="#B5B5B5" stroke-miterlimit="10" stroke-width="1.643" d="M295.803 149.728h307v-33.172"/>
    <path fill="#B5B5B5" d="M606.899 117.754l-4.096-7.092-4.095 7.092z"/>
    <path fill="none" stroke="#B5B5B5" stroke-miterlimit="10" stroke-width="1.643" d="M295.803 179.728h42.144v131.958h-42.144M337.947 243.207h47.683"/>
    <path fill="#B5B5B5" d="M384.432 247.303l7.092-4.096-7.092-4.095z"/>
    <path fill="none" stroke="#B5B5B5" stroke-miterlimit="10" stroke-width="1.643" d="M301.698 135.346h35.105V48.454h48.827"/>
    <path fill="#B5B5B5" d="M302.896 139.442l-7.093-4.096 7.093-4.095zM384.432 52.55l7.092-4.096-7.092-4.095z"/>
    <path fill="none" stroke="#B5B5B5" stroke-miterlimit="10" stroke-width="1.643" d="M301.698 165.346h302.106v38.478"/>
    <path fill="#B5B5B5" d="M302.896 169.442l-7.093-4.096 7.093-4.095zM599.708 202.625l4.096 7.093 4.095-7.093z"/>
    <path d="M4.209 181.653a3.01 3.01 0 003.01 3.01H76.2a3.01 3.01 0 003.01-3.01V134.66h-75l-.001 46.993z" fill="#59B4D9"/>
    <path d="M76.2 120.713H7.219a3.009 3.009 0 00-3.01 3.008v15.943h75v-15.94a3.01 3.01 0 00-3.009-3.011s-.001 0 0 0" fill="#A0A1A2"/>
    <path d="M7.23 120.713a3.01 3.01 0 00-3.01 3.01v57.931a3.012 3.012 0 003.01 3.01h3.282l59.127-63.951H7.23z" fill="#FFF" opacity=".2"/>
    <path fill="#FFF" d="M23.494 127.881H74v5.913H23.494z"/>
    <path d="M21.174 130.737a7.317 7.317 0 11-14.634-.004 7.317 7.317 0 0114.634.004" fill="#59B4D9"/>
    <path fill="#FFF" d="M13.083 131.561l3.319 3.504h-1.801l-4.439-4.227 4.422-4.227h1.797l-3.298 3.483h8.089v1.467z"/>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(19.615 215.904)">
        Browser
    </text>
    <path fill="none" d="M0 115.383h83.417v104.309H0z"/>
    <path d="M567.085 278.8a2.756 2.756 0 002.85 2.85h69.3a2.756 2.756 0 002.85-2.85v-49.65h-75v49.65z" fill="#A0A1A2"/>
    <path d="M639.235 217.754h-69.3a2.756 2.756 0 00-2.85 2.85v8.55h75V220.6a2.756 2.756 0 00-2.85-2.85" fill="#7A7A7A"/>
    <path fill="#FFF" d="M595.285 234.104h18.9v11.4h-18.9z"/>
    <path fill="#FCD116" d="M595.285 249.554h18.9v11.4h-18.9zM617.785 249.554h18.9v11.4h-18.9z"/>
    <path fill="#FFF" d="M617.785 234.104h18.9v11.4h-18.9zM572.785 234.104h18.9v11.4h-18.9zM572.785 249.554h18.9v11.4h-18.9z"/>
    <path fill="#FCD116" d="M572.785 264.854h18.9v11.4h-18.9zM595.285 264.854h18.9v11.4h-18.9zM617.785 264.854h18.9v11.4h-18.9z"/>
    <path d="M569.935 217.754a3.065 3.065 0 00-2.85 2.85v58.2a3.065 3.065 0 002.85 2.85h3.15l59.4-63.9h-62.55z" fill="#FFF" opacity=".2"/>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(581.563 308.072)">
        S
    </text>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(587.551 308.072)">
        torage
    </text>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(556.842 322.472)">
        (media, logs, and
    </text>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(568.737 336.872)">
        backup files)
    </text>
    <path fill="none" d="M562.876 216.399h83.417v123.885h-83.417z"/>
    <path d="M626.569 25.962v-.451c0-11.57-9.918-21.187-22.089-21.338-.3-.451-7.213.15-7.213.15-10.967 1.353-19.535 10.519-19.535 21.188 0 .3-1.2 8.715 7.363 15.778 3.907 3.456 7.964 12.773 8.565 15.477l.451.9h15.928l.451-.9c.6-2.7 4.809-12.021 8.565-15.327 8.566-7.213 7.514-15.177 7.514-15.477z" fill="#68217A"/>
    <path fill="#7A7A7A" d="M594.412 63.077h15.928v5.109h-15.928zM599.371 79.006h5.86l4.959-5.26h-15.778z"/>
    <path d="M606.283 56.917h-3.005V37.833h-2.555v18.933h-3.005V37.833h-2.555a5.646 5.646 0 01-5.56-5.56 5.56 5.56 0 0111.12 0v2.555h2.555v-2.555a5.56 5.56 0 115.56 5.56h-2.555v19.084zm-11.12-27.2a2.533 2.533 0 00-2.555 2.511v.044a2.633 2.633 0 002.555 2.555h2.555v-2.554a2.745 2.745 0 00-2.555-2.555v-.001zm13.674 0a2.633 2.633 0 00-2.555 2.555v2.555h2.555a2.633 2.633 0 002.555-2.555 2.533 2.533 0 00-2.512-2.554h-.043v-.001z" fill="#FFF" opacity=".65"/>
    <path d="M604.48 4.173c-.3-.451-7.213.15-7.213.15-10.967 1.353-19.535 10.519-19.535 21.188 0 .3-1.052 7.664 5.86 14.426L616.05 7.479a22.074 22.074 0 00-11.57-3.306z" fill="#FFF" opacity=".15"/>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(551.185 101.317)">
        Application Insights
    </text>
    <path fill="none" d="M570.785 0h63.9v104.309h-63.9z"/>
    <g>
        <path d="M407.387 20.243v50.845c0 5.352 11.831 9.577 26.338 9.577V20.243h-26.338z" fill="#3999C6"/>
        <path d="M433.444 80.666h.423c14.648 0 26.338-4.225 26.338-9.577V20.243h-26.761v60.423z" fill="#59B4D9"/>
        <path d="M460.2 20.243c0 5.211-11.831 9.577-26.338 9.577s-26.479-4.366-26.479-9.577 11.831-9.577 26.338-9.577 26.479 4.366 26.479 9.577" fill="#FFF"/>
        <path d="M454.852 19.68c0 3.521-9.437 6.338-20.986 6.338s-21.127-2.818-21.127-6.338 9.437-6.338 20.986-6.338 21.127 2.817 21.127 6.338" fill="#7FBA00"/>
        <path d="M450.345 23.482c2.817-1.127 4.366-2.394 4.366-3.8 0-3.521-9.437-6.338-20.986-6.338s-20.986 2.817-20.986 6.338c0 1.408 1.69 2.817 4.366 3.8 3.8-1.549 9.859-2.394 16.62-2.394s12.817.986 16.62 2.394" fill="#B8D432"/>
        <path d="M440.908 40.384v33.944c0 3.521 7.887 6.338 17.606 6.338V40.384h-17.606z" fill="#0072C6"/>
        <path d="M458.232 80.666h.282c9.718 0 17.606-2.817 17.606-6.338V40.384h-17.888v40.282z" fill="#0072C6"/>
        <path d="M458.232 80.666h.282c9.718 0 17.606-2.817 17.606-6.338V40.384h-17.888v40.282z" fill="#FFF" opacity=".15"/>
        <path d="M476.12 40.384c0 3.521-7.887 6.338-17.606 6.338s-17.606-2.817-17.606-6.338 7.887-6.338 17.606-6.338 17.606 2.817 17.606 6.338" fill="#FFF"/>
        <path d="M472.458 39.961c0 2.254-6.338 4.225-13.944 4.225s-13.944-1.831-13.944-4.225c0-2.254 6.338-4.225 13.944-4.225s13.944 1.972 13.944 4.225" fill="#7FBA00"/>
        <path d="M469.5 42.5c1.831-.7 2.958-1.549 2.958-2.535 0-2.254-6.338-4.225-13.944-4.225-7.746 0-13.944 1.831-13.944 4.225 0 .986 1.127 1.831 2.958 2.535a36.542 36.542 0 0121.972 0" fill="#B8D432"/>
        <path fill="#FFF" d="M468.091 60.947l-19.577 16.197 7.606-12.535h-6.62l19.577-16.056-7.605 12.394z"/>
    </g>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(409.109 100.638)">
        R
    </text>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(415.935 100.638)">
        edis Cache
    </text>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(393.245 115.038)">
        (Session state and
    </text>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(404.424 129.438)">
        output cache)
    </text>
    <path fill="none" d="M398.903 7.177h83.417V134.66h-83.417z"/>
    <g>
        <path d="M413.85 220.829v54.507c0 5.659 12.667 10.247 28.291 10.247v-64.754H413.85z" fill="#0072C6"/>
        <path d="M441.753 285.582h.388c15.624 0 28.291-4.586 28.291-10.246v-54.507h-28.679v64.753z" fill="#0072C6"/>
        <path d="M441.753 285.582h.388c15.624 0 28.291-4.586 28.291-10.246v-54.507h-28.679v64.753z" fill="#FFF" opacity=".15"/>
        <path d="M470.432 220.829c0 5.659-12.667 10.246-28.291 10.246s-28.291-4.587-28.291-10.246 12.667-10.246 28.291-10.246 28.291 4.587 28.291 10.246" fill="#FFF"/>
        <path d="M464.648 220.239c0 3.736-10.077 6.761-22.507 6.761s-22.508-3.025-22.508-6.761 10.078-6.761 22.508-6.761 22.507 3.026 22.507 6.761" fill="#7FBA00"/>
        <path d="M459.933 224.371c2.946-1.143 4.717-2.574 4.717-4.128 0-3.736-10.077-6.762-22.508-6.762s-22.507 3.026-22.507 6.762c0 1.555 1.771 2.986 4.717 4.128 4.115-1.6 10.545-2.628 17.79-2.628s13.674 1.031 17.792 2.628" fill="#B8D432"/>
        <path d="M433.156 258.664a4.644 4.644 0 01-1.843 3.935 8.265 8.265 0 01-5.091 1.395 9.687 9.687 0 01-4.62-1v-3.985a7.13 7.13 0 004.718 1.819 3.216 3.216 0 001.925-.5c.435-.297.691-.794.679-1.321a1.847 1.847 0 00-.654-1.407 12.044 12.044 0 00-2.658-1.544c-2.723-1.277-4.084-3.02-4.084-5.229a4.72 4.72 0 011.781-3.854 7.268 7.268 0 014.731-1.451 11.818 11.818 0 014.334.685v3.722a7.067 7.067 0 00-4.109-1.245 3.044 3.044 0 00-1.829.491 1.55 1.55 0 00-.672 1.313 1.875 1.875 0 00.542 1.389 8.775 8.775 0 002.222 1.339 11.005 11.005 0 013.568 2.4 4.477 4.477 0 011.06 3.048zM452.366 254.631a10.183 10.183 0 01-1.432 5.466 7.64 7.64 0 01-4.033 3.25l5.179 4.794h-5.229l-3.7-4.146a8.672 8.672 0 01-4.29-1.257 7.883 7.883 0 01-2.951-3.206 9.833 9.833 0 01-1.04-4.539 10.6 10.6 0 011.13-4.95 7.997 7.997 0 013.168-3.343 9.256 9.256 0 014.682-1.17 8.62 8.62 0 014.414 1.134 7.728 7.728 0 013.025 3.224 10.186 10.186 0 011.077 4.743zm-4.232.225a6.988 6.988 0 00-1.183-4.29 3.829 3.829 0 00-3.238-1.576 4.066 4.066 0 00-3.349 1.58 7.685 7.685 0 00-.026 8.385 3.961 3.961 0 003.274 1.562 4.015 4.015 0 003.3-1.512 6.418 6.418 0 001.222-4.149zM465.949 263.683h-10.632V245.83h4.021v14.591h6.611z" fill="#FFF"/>
    </g>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(405.353 307.831)">
        SQL Database
    </text>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(393.53 322.231)">
        (Umbraco DB and
    </text>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(396.813 336.631)">
        Session state DB)
    </text>
    <path fill="none" d="M406.425 208.84h73.217v131.445h-73.217z"/>
    <g>
        <path d="M263.679 172.85c-15.344 11.751-37.308 8.838-49.058-6.506s-8.838-37.308 6.506-49.058 37.308-8.838 49.058 6.506l.012.016c11.756 15.245 8.927 37.133-6.318 48.889l-.2.153" fill="#59B4D9"/>
        <path d="M257.249 151.2a7.54 7.54 0 0010.557 1.406c.172-.132.305-.291.462-.433 3.373 2.376 5.715 3.944 7.035 4.843.365-.983.678-1.984.938-3-1.394-1.037-3.28-2.489-6.006-4.7a7.476 7.476 0 00-10.732-9.167c-3.564-3.2-7.48-6.863-11.61-10.966 12.831-6.9 21.946-5.89 21.946-5.89a35.143 35.143 0 00-5.048-5.176c-5.411-.836-13.817-.742-23.421 4.367-3.2-3.35-6.459-6.95-9.776-10.8a32.549 32.549 0 00-4.637 1.886 75.379 75.379 0 009.456 11.991l.024.024a64.824 64.824 0 00-9.722 8.421c-.406.433-.8.868-1.179 1.3a10.566 10.566 0 00-5.764.395c-3.17-6.839-2.915-12.333-2.414-15.165a36.934 36.934 0 00-3.769 4.574 22.417 22.417 0 001.379 14.133 10.553 10.553 0 00-.007 12.814c.244.314.506.615.783.9a53.029 53.029 0 00-2.044 12.265c.332.451.332.815.661 1.254a35.507 35.507 0 005.824 5.611 38.57 38.57 0 012.4-15.921 10.507 10.507 0 004.876-.792c.9.788 1.834 1.585 2.835 2.4a58.343 58.343 0 0010.2 6.5 6.918 6.918 0 0011.131 6.212 6.88 6.88 0 001.551-1.7 62.473 62.473 0 0013.728 1.427c.54 0 3.048-3.41 4.484-5.524-2.148.449-8.516 1.324-17.22-1.176a6.878 6.878 0 00-10.522-4.358 65.635 65.635 0 01-9.461-6.286 62.55 62.55 0 01-1.9-1.565 10.61 10.61 0 00.445-10.57c.4-.4.794-.8 1.219-1.2a76.938 76.938 0 019.127-7.384c-.115-.106-.218-.218-.33-.326.113.1.22.213.335.318 4.369 4.04 9 7.869 13.39 11.291a7.486 7.486 0 00.776 7.767z" fill="#FFF"/>
    </g>
    <circle cx="263.679" cy="172.707" fill="#FFF" r="27"/>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(220.835 215.576)">
        W
    </text>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(231.575 215.576)">
        eb App
    </text>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(191.904 229.976)">
        (Umbraco Frontend)
    </text>
    <path d="M238.679 172.737c.017-13.807 11.224-24.986 25.031-24.969 13.807.017 24.986 11.224 24.969 25.031-.017 13.795-11.205 24.969-25 24.969-13.815-.008-25.008-11.215-25-25.03v-.001zm24.492 8.561a24.565 24.565 0 01-5.775-.521 4.42 4.42 0 01-3.158-2.538 15.306 15.306 0 01-.824-6.025c.01-1.42.099-2.838.265-4.248.164-1.371.328-2.504.491-3.4l.172-.888a.508.508 0 00-.415-.58l-3.231-.5a.508.508 0 00-.575.385c-.053.207-.087.361-.184.853a56.828 56.828 0 00-.544 3.207 41.987 41.987 0 00-.364 4.424 22.907 22.907 0 000 3.1 15.043 15.043 0 001.411 6.557 7.465 7.465 0 004.387 3.53 26.906 26.906 0 008.613 1.054h.478a26.906 26.906 0 008.613-1.054 7.465 7.465 0 004.387-3.53 15.057 15.057 0 001.411-6.557c.07-1.032.07-2.068 0-3.1a41.987 41.987 0 00-.364-4.424 55.782 55.782 0 00-.544-3.207c-.1-.492-.13-.646-.183-.853a.51.51 0 00-.581-.385l-3.23.5a.508.508 0 00-.416.58l.172.888c.163.893.327 2.027.491 3.4.167 1.41.255 2.828.265 4.248a15.324 15.324 0 01-.824 6.025 4.42 4.42 0 01-3.158 2.538 24.565 24.565 0 01-5.775.521h-1.011z" fill="#FF6E00"/>
    <path fill="none" d="M201.955 107.507h88.724v126.597h-88.724z"/>
    <g>
        <path d="M263.679 341.035c-15.344 11.751-37.308 8.838-49.058-6.506-11.751-15.344-8.838-37.308 6.506-49.058s37.308-8.838 49.058 6.506l.012.016c11.756 15.245 8.927 37.133-6.318 48.889l-.2.153" fill="#59B4D9"/>
        <path d="M257.249 319.39a7.54 7.54 0 0010.557 1.406c.172-.132.305-.291.462-.433 3.373 2.376 5.715 3.944 7.035 4.843.365-.983.678-1.984.938-3-1.394-1.037-3.28-2.489-6.006-4.7a7.476 7.476 0 00-10.732-9.167c-3.564-3.2-7.48-6.863-11.61-10.966 12.831-6.9 21.946-5.89 21.946-5.89a35.143 35.143 0 00-5.048-5.176c-5.411-.836-13.817-.742-23.421 4.367-3.2-3.35-6.459-6.95-9.776-10.8a32.549 32.549 0 00-4.637 1.886 75.379 75.379 0 009.456 11.991l.024.024a64.824 64.824 0 00-9.722 8.421c-.406.433-.8.868-1.179 1.3a10.566 10.566 0 00-5.764.395c-3.17-6.839-2.915-12.333-2.414-15.165a36.934 36.934 0 00-3.769 4.574 22.417 22.417 0 001.379 14.133 10.553 10.553 0 00-.007 12.814c.244.314.506.615.783.9a53.029 53.029 0 00-2.044 12.265c.332.451.332.815.661 1.254a35.507 35.507 0 005.824 5.611 38.57 38.57 0 012.4-15.921 10.507 10.507 0 004.876-.792c.9.788 1.834 1.585 2.835 2.4a58.343 58.343 0 0010.2 6.5 6.918 6.918 0 0011.131 6.212 6.88 6.88 0 001.551-1.7A62.417 62.417 0 00266.9 338.4c.54 0 3.048-3.41 4.484-5.524-2.148.449-8.516 1.324-17.22-1.176a6.878 6.878 0 00-10.522-4.358 65.635 65.635 0 01-9.461-6.286 62.55 62.55 0 01-1.9-1.565 10.61 10.61 0 00.445-10.57c.4-.4.794-.8 1.219-1.2a76.938 76.938 0 019.127-7.384c-.115-.106-.218-.218-.33-.326.113.1.22.213.335.318 4.369 4.04 9 7.869 13.39 11.291a7.486 7.486 0 00.782 7.77z" fill="#FFF"/>
    </g>
    <circle cx="263.679" cy="340.892" fill="#FFF" r="27"/>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(220.835 383.756)">
        W
    </text>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(231.575 383.756)">
        eb App
    </text>
    <text fill="#5D5D5D" font-family="'Segoe UI'" font-size="12" transform="translate(198.511 398.156)">
        (Umbraco Admin)
    </text>
    <path d="M238.679 340.86c.017-13.807 11.224-24.986 25.031-24.969 13.807.017 24.986 11.224 24.969 25.031-.017 13.795-11.205 24.969-25 24.969-13.815-.008-25.008-11.215-25-25.03v-.001zm24.492 8.561a24.565 24.565 0 01-5.775-.521 4.42 4.42 0 01-3.158-2.538 15.306 15.306 0 01-.824-6.025c.01-1.42.099-2.838.265-4.248.164-1.371.328-2.504.491-3.4l.172-.888a.508.508 0 00-.415-.58l-3.231-.5a.508.508 0 00-.575.385c-.053.207-.087.361-.184.853a56.828 56.828 0 00-.544 3.207 41.987 41.987 0 00-.364 4.424 22.907 22.907 0 000 3.1 15.043 15.043 0 001.411 6.557 7.465 7.465 0 004.387 3.53 26.906 26.906 0 008.613 1.054h.478a26.906 26.906 0 008.613-1.054 7.465 7.465 0 004.387-3.53 15.057 15.057 0 001.411-6.557c.07-1.032.07-2.068 0-3.1a41.987 41.987 0 00-.364-4.424 55.782 55.782 0 00-.544-3.207c-.1-.492-.13-.646-.183-.853a.51.51 0 00-.581-.385l-3.23.5a.508.508 0 00-.416.58l.172.888c.163.893.327 2.027.491 3.4.167 1.41.255 2.828.265 4.248a15.324 15.324 0 01-.824 6.025 4.42 4.42 0 01-3.158 2.538 24.565 24.565 0 01-5.775.521h-1.011z" fill="#FF6E00"/>
    <path fill="none" d="M201.955 274.299h88.724v126.597h-88.724z"/>
</svg>

## Deploy to Azure

Use the following pre-built template to deploy this architecture to Azure

[Deploy to Azure](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fumbraco-cms-webapp-redis-cache%2Fazuredeploy.json)

[View template source](https://azure.microsoft.com/resources/templates/umbraco-cms-webapp-redis-cache/)

## Components
* Run an Umbraco CMS on the [Web Apps](https://azure.microsoft.com/services/app-service/web/) feature of Azure App Service with the front-end and back-office apps running on the same app.
* Store your site’s content in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/). The back-office web app and front-end web app use the same database. Use [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)’s features such as backup and high availability.
* [Storage Accounts](https://azure.microsoft.com/services/storage/): Store all your media in Azure Storage, so you can reduce I/O operation on the web app file server and improve performance.
* Application Insights: Detect issues, diagnose crashes, and track usage in your web app with Application Insights. Make informed decisions throughout the development lifecycle.
* Store session state and output cache on [Azure Cache for Redis](https://azure.microsoft.com/services/cache/) to improve performance and reduce the load on your web front ends.

## Next Steps
* [Create a web app from the Azure Marketplace](/api/Redirect/documentation/articles/app-service-web-create-web-app-from-marketplace/)
* [SQL Database tutorial: Create a SQL database in minutes by using the Azure portal](/api/Redirect/documentation/articles/sql-database-get-started/)
* [Get started with Azure Blob storage using .NET](/api/Redirect/documentation/articles/storage-dotnet-how-to-use-blobs/)
* [Logs, exceptions and custom diagnostics for ASP.NET in Application Insights](/api/Redirect/documentation/articles/app-insights-search-diagnostic-logs/)
* [How to create a Web App with Azure Cache for Redis](/api/Redirect/documentation/articles/cache-web-app-howto/)

## Deploy to Azure
* [Deploy to Azure](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fumbraco-cms-webapp-redis-cache%2Fazuredeploy.json)


