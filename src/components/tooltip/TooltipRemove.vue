<template>
  <div class="tooltip-remove"
       tabindex="-1"
       v-autofocus
       v-click-outside="focusOut"
  >
    <button class="tooltip-remove__close" @click="closeTooltip"></button>
    <div class="tooltip-remove__header">
      <span>{{ !editing ? "Форматирование" : "Личный Объем"}}</span>
    </div>
    <div class="tooltip-remove__body">
      <div v-if="!editing">
        <div v-if="card.list.length"
             class="tooltip-remove__row"
        >
          <div class="tooltip-remove__label" @click.once="deleteChildren">
          <span class="tooltip-remove__icon">
            <svg height="100%" viewBox="-64 0 512 512" width="100%"
                 xmlns="http://www.w3.org/2000/svg"><path
              d="m256 80h-32v-48h-64v48h-32v-80h128zm0 0" fill="#62808c"/><path
              d="m304 512h-224c-26.507812 0-48-21.492188-48-48v-336h320v336c0 26.507812-21.492188 48-48 48zm0 0"
              fill="#e76e54"/><path
              d="m384 160h-384v-64c0-17.671875 14.328125-32 32-32h320c17.671875 0 32 14.328125 32 32zm0 0"
              fill="#77959e"/><path
              d="m260 260c-6.246094-6.246094-16.375-6.246094-22.625 0l-41.375 41.375-41.375-41.375c-6.25-6.246094-16.378906-6.246094-22.625 0s-6.246094 16.375 0 22.625l41.375 41.375-41.375 41.375c-6.246094 6.25-6.246094 16.378906 0 22.625s16.375 6.246094 22.625 0l41.375-41.375 41.375 41.375c6.25 6.246094 16.378906 6.246094 22.625 0s6.246094-16.375 0-22.625l-41.375-41.375 41.375-41.375c6.246094-6.25 6.246094-16.378906 0-22.625zm0 0"
              fill="#fff"/></svg></span>
            <span>Удалить ветку</span>
          </div>
        </div>
        <div class="tooltip-remove__row"
             v-if="!card.root"
        >
          <div class="tooltip-remove__label"
               @click.once="deleteCardWithChildren"
          >
          <span class="tooltip-remove__icon">
            <svg id="Layer_1" enable-background="new 0 0 512 512" height="100%" viewBox="0 0 512 512" width="100%"
                 xmlns="http://www.w3.org/2000/svg"><path
              d="m278.068 27.55c-9.959 0-19.204 3.035-26.861 8.222 2.773 7.613 4.213 16.379 4.213 26.214v14.09c41.374 9.204 70.474 33.612 70.474 79.918v-80.806c0-26.31-21.413-47.638-47.826-47.638z"
              fill="#3d5959"/><path
              d="m211.64 71.689c15.895 0 31.028 1.455 44.78 4.611v-14.313c0-39.306-22.606-61.987-62.066-61.987h-25.518c-39.462 0-71.451 31.864-71.451 71.17v84.825c0-61.398 51.152-84.306 114.255-84.306z"
              fill="#537982"/><path
              d="m129.932 91.43v-20.26c0-38.254 30.304-69.449 68.304-71.09-1.276-.051-2.569-.08-3.882-.08h-25.518c-39.462 0-71.451 31.864-71.451 71.17v84.825c0-30.24 12.414-51.137 32.547-64.565z"
              fill="#3d5959"/><path
              d="m312.394 350.47h-48.242v1c-3.411 25.824-25.788 45.162-52.512 45.162-26.723 0-49.1-19.338-52.512-45.162v-1h-77.858c-27.887 0-50.576 22.135-50.576 49.34v72.938c0 3.619 2.979 6.554 6.653 6.554h274.973c-15.479-17.048-24.919-39.633-24.919-64.375-.001-24.78 9.469-47.4 24.993-64.457z"
              fill="#fda613"/><path
              d="m73.658 472.749v-72.939c0-27.206 22.689-49.34 50.576-49.34h-42.964c-27.887 0-50.576 22.135-50.576 49.34v72.938c0 3.619 2.979 6.554 6.653 6.554h42.965c-3.675.001-6.654-2.935-6.654-6.553z"
              fill="#fa8701"/><path
              d="m243.561 316.234c-6.032 1.114-12.253 1.704-18.612 1.704h-26.62c-6.358 0-12.578-.59-18.61-1.704v34.235h-21.72c2.924 26.517 25.819 47.162 53.641 47.162 27.821 0 50.718-20.645 53.64-47.162h-21.718v-34.235z"
              fill="#ffaf9d"/><path
              d="m198.329 317.939c-6.358 0-12.578-.59-18.61-1.704v34.235h-21.72c1.251 11.352 6.172 21.621 13.565 29.662h33.08c2.846 0 5.151-2.307 5.151-5.151v-57.042z"
              fill="#f69380"/><path
              d="m98.385 220.331v-50.708h-16.572c-11.594 0-20.998 9.089-20.998 20.299v24.574c0 11.211 9.404 20.299 20.998 20.299h17.671c-.721-4.722-1.099-9.55-1.099-14.464z"
              fill="#ffcdbe"/><path
              d="m341.469 169.623h-16.575v50.708c0 4.913-.378 9.742-1.099 14.463h17.674c11.598 0 20.995-9.088 20.995-20.299v-24.574c0-11.21-9.398-20.298-20.995-20.298z"
              fill="#ffaf9d"/><path
              d="m211.64 70.628c-63.103 0-114.255 22.907-114.255 84.306v65.398c0 54.458 45.194 98.607 100.944 98.607h26.62c55.751 0 100.944-44.15 100.944-98.607v-65.398c.001-61.399-51.153-84.306-114.253-84.306z"
              fill="#ffcdbe"/><path
              d="m129.48 220.331v-65.398c0-56.098 42.704-80.06 98.208-83.779-5.245-.352-10.6-.526-16.048-.526-63.103 0-114.255 22.907-114.255 84.306v65.398c0 54.458 45.194 98.607 100.944 98.607h26.62c.916 0 1.827-.014 2.736-.037-54.483-1.418-98.205-45.007-98.205-98.571z"
              fill="#ffaf9d"/><g fill="#ab5e2e"><path
              d="m222.138 220.232h-13.805c-7.684 0-13.935-6.181-13.935-13.778v-31.966c0-4.142 3.357-7.5 7.5-7.5s7.5 3.358 7.5 7.5v30.744h12.739c4.143 0 7.5 3.358 7.5 7.5.001 4.142-3.357 7.5-7.499 7.5z"/><path
              d="m150.435 194.748c-4.143 0-7.5-3.358-7.5-7.5v-22.695c0-4.142 3.357-7.5 7.5-7.5s7.5 3.358 7.5 7.5v22.695c0 4.142-3.358 7.5-7.5 7.5z"/><path
              d="m272.844 194.748c-4.143 0-7.5-3.358-7.5-7.5v-22.695c0-4.142 3.357-7.5 7.5-7.5 4.142 0 7.5 3.358 7.5 7.5v22.695c0 4.142-3.358 7.5-7.5 7.5z"/></g><ellipse
              cx="383.853" cy="414.928" fill="#fd646f" rx="97.453" ry="97.072"/><path
              d="m318.639 414.928c0-48.141 35.185-88.089 81.334-95.742-5.244-.87-10.628-1.329-16.119-1.329-53.821 0-97.453 43.461-97.453 97.072 0 53.61 43.632 97.072 97.453 97.072 5.491 0 10.875-.46 16.119-1.33-46.15-7.653-81.334-47.603-81.334-95.743z"
              fill="#fc4755"/><path
              d="m412.603 463.965c-1.35 1.351-3.534 1.355-4.879.011l-24.066-24.066-24.452 24.452c-1.35 1.35-3.534 1.354-4.879.009l-19.917-19.915c-1.345-1.345-1.341-3.529.011-4.879l24.451-24.453-24.066-24.065c-1.344-1.345-1.34-3.529.01-4.88l20.29-20.289c1.352-1.351 3.535-1.355 4.88-.01l24.066 24.065 24.451-24.452c1.351-1.351 3.534-1.354 4.879-.009l19.917 19.915c1.345 1.345 1.34 3.529-.01 4.879l-24.452 24.453 24.066 24.066c1.345 1.344 1.34 3.528-.011 4.879z"
              fill="#fff"/><path
              d="m172.225 280.704c-1.042 0-2.101-.218-3.11-.68-3.769-1.721-5.428-6.17-3.707-9.938 8.232-18.025 26.379-29.673 46.232-29.673 19.852 0 37.999 11.647 46.232 29.673 1.721 3.768.061 8.217-3.706 9.938-3.77 1.721-8.217.061-9.938-3.707-5.8-12.699-18.592-20.904-32.588-20.904-13.997 0-26.788 8.206-32.587 20.904-1.261 2.759-3.983 4.387-6.828 4.387z"
              fill="#ab5e2e"/></svg></span>
            <span>Удалить партнера и ветку</span>
          </div>
        </div>
        <div class="tooltip-remove__row">
          <div class="tooltip-remove__label"
               @click.once="editPersonalVolume"
               v-if="!editing"
          >
          <span class="tooltip-remove__icon">
            <svg width="100%" height="100%" xmlns="http://www.w3.org/2000/svg"
                 xmlns:xlink="http://www.w3.org/1999/xlink"
                 version="1.1"
                 id="Capa_1" x="0px" y="0px" viewBox="0 0 512.001 512.001"
                 style="enable-background:new 0 0 512.001 512.001;" xml:space="preserve">
<path style="fill:#C2CECE;"
      d="M374.995,512H6.009c-2.337,0-4.233-1.894-4.233-4.233v-5.412c0-5.327,4.318-9.645,9.645-9.645  h363.572c5.327,0,9.645,4.318,9.645,9.645l0,0C384.639,507.681,380.32,512,374.995,512z"/>
<linearGradient id="SVGID_1_" gradientUnits="userSpaceOnUse" x1="122.9393" y1="31.6691" x2="-31.1507" y2="185.7591"
                gradientTransform="matrix(1.0667 0 0 -1.0667 3.2666 557.5336)">
	<stop offset="0" style="stop-color:#FFCF95"/>
	<stop offset="0.054" style="stop-color:#FED19A"/>
	<stop offset="1" style="stop-color:#E8EFEE"/>
</linearGradient>
<path style="fill:url(#SVGID_1_);"
      d="M120.736,391.264L70.42,340.947l-16.864,16.864c-5.104,5.104-8.941,11.334-11.2,18.19  L0.337,503.464c-1.669,5.062,3.137,9.869,8.199,8.199l127.462-42.018c6.855-2.26,13.086-6.096,18.19-11.2l16.864-16.864  L120.736,391.264z"/>
<linearGradient id="SVGID_2_" gradientUnits="userSpaceOnUse" x1="75.6716" y1="82.2689" x2="83.6716" y2="59.8689"
                gradientTransform="matrix(1.0667 0 0 -1.0667 3.2666 557.5336)">
	<stop offset="0" style="stop-color:#C69C6D;stop-opacity:0"/>
	<stop offset="1" style="stop-color:#754C24"/>
</linearGradient>
<path style="fill:url(#SVGID_2_);"
      d="M154.189,435.721c-5.104,5.104-11.334,8.941-18.19,11.2L8.537,488.939  c-1.199,0.395-2.38,0.417-3.467,0.17l-4.733,14.355c-1.669,5.062,3.137,9.869,8.199,8.199l127.462-42.018  c6.855-2.26,13.086-6.096,18.19-11.2l16.864-16.864l-11.362-11.362L154.189,435.721z"/>
<linearGradient id="SVGID_3_" gradientUnits="userSpaceOnUse" x1="286.5774" y1="208.2871" x2="203.0874" y2="291.7771"
                gradientTransform="matrix(1.0667 0 0 -1.0667 3.2666 557.5336)">
	<stop offset="0" style="stop-color:#FF9102"/>
	<stop offset="1" style="stop-color:#FFC200"/>
</linearGradient>
<path style="fill:url(#SVGID_3_);"
      d="M150.963,461.671c4.562-4.562,6.844-10.55,6.844-16.539c0-5.963-2.282-11.951-6.844-16.513  l-0.493-0.493c-5.495-5.495-13.039-7.674-20.169-6.559c-1.854,0.299-3.578-0.363-4.77-1.555c-1.193-1.193-1.841-2.903-1.555-4.743  c-0.013-0.013,0-0.026,0-0.026c0.078-0.466,0.129-0.933,0.181-1.4c0.013-0.246,0.038-0.48,0.052-0.725  c0.038-0.506,0.052-1.011,0.052-1.53c0-5.963-2.282-11.951-6.844-16.513l-0.493-0.493c-0.285-0.285-0.583-0.557-0.881-0.83  c-0.246-0.221-0.506-0.453-0.765-0.661c-0.402-0.35-0.817-0.661-1.245-0.959c-0.221-0.169-0.466-0.337-0.7-0.493  c-0.337-0.234-0.7-0.466-1.062-0.674c-0.35-0.194-0.687-0.375-1.024-0.557c-0.453-0.246-0.908-0.466-1.361-0.661  c-0.375-0.169-0.765-0.324-1.14-0.467c-0.35-0.143-0.713-0.272-1.089-0.388c-0.921-0.299-1.867-0.544-2.826-0.725  c-0.453-0.091-0.894-0.169-1.335-0.221c-0.453-0.065-0.908-0.103-1.348-0.129c-0.453-0.038-0.894-0.065-1.361-0.065  c-0.453-0.013-0.894-0.013-1.335,0.013c-0.921,0.038-1.802,0.116-2.697,0.259c-1.854,0.299-3.578-0.363-4.77-1.555  c-1.193-1.193-1.854-2.916-1.555-4.77c0.194-1.205,0.285-2.436,0.285-3.655c0-5.963-2.282-11.951-6.844-16.513l-0.493-0.493  c-9.125-9.125-23.927-9.125-33.052,0L334.625,76.738l100.634,100.634L150.963,461.671z"/>
<linearGradient id="SVGID_4_" gradientUnits="userSpaceOnUse" x1="212.0359" y1="290.4356" x2="243.8259" y2="258.6456"
                gradientTransform="matrix(1.0667 0 0 -1.0667 3.2666 557.5336)">
	<stop offset="0" style="stop-color:#FFCF95"/>
	<stop offset="0.427" style="stop-color:#FFC954"/>
	<stop offset="1" style="stop-color:#FFC200"/>
</linearGradient>
<path style="fill:url(#SVGID_4_);"
      d="M401.717,143.828L125.532,420.013c-1.193-1.193-1.841-2.903-1.555-4.743  c-0.013-0.013,0-0.026,0-0.026c0.078-0.466,0.129-0.933,0.181-1.399c0.013-0.246,0.038-0.48,0.052-0.725  c0.038-0.506,0.052-1.011,0.052-1.53c0-5.963-2.282-11.951-6.844-16.513l-0.493-0.493c-0.285-0.285-0.583-0.557-0.881-0.83  c-0.246-0.221-0.506-0.453-0.765-0.661c-0.402-0.35-0.817-0.661-1.245-0.959c-0.234-0.181-0.466-0.337-0.7-0.493  c-0.337-0.234-0.7-0.466-1.062-0.674c-0.337-0.181-0.674-0.389-1.024-0.557c-0.453-0.246-0.908-0.466-1.361-0.661  c-0.375-0.169-0.765-0.324-1.14-0.467c-0.35-0.143-0.713-0.272-1.089-0.388c-0.921-0.299-1.867-0.544-2.826-0.725  c-0.428-0.091-0.881-0.156-1.335-0.221c-0.441-0.052-0.881-0.103-1.348-0.129c-0.441-0.052-0.894-0.065-1.361-0.065  c-0.453-0.013-0.908,0-1.335,0.013c-0.921,0.038-1.802,0.116-2.697,0.259c-1.854,0.299-3.578-0.363-4.77-1.555l276.185-276.185  L401.717,143.828z"/>
<linearGradient id="SVGID_5_" gradientUnits="userSpaceOnUse" x1="187.8979" y1="306.9676" x2="208.5179" y2="286.3476"
                gradientTransform="matrix(1.0667 0 0 -1.0667 3.2666 557.5336)">
	<stop offset="0" style="stop-color:#FFCF95"/>
	<stop offset="0.427" style="stop-color:#FFC954"/>
	<stop offset="1" style="stop-color:#FFC200"/>
</linearGradient>
<path style="fill:url(#SVGID_5_);"
      d="M334.628,76.739L50.329,361.038c9.125-9.125,23.927-9.125,33.052,0l0.493,0.493  c4.562,4.562,6.844,10.55,6.844,16.513c0,1.218-0.091,2.45-0.285,3.655c-0.298,1.854,0.363,3.578,1.555,4.77l276.185-276.185  L334.628,76.739z"/>
<linearGradient id="SVGID_6_" gradientUnits="userSpaceOnUse" x1="432.3438" y1="478.0998" x2="397.4038" y2="443.1518"
                gradientTransform="matrix(1.0667 0 0 -1.0667 3.2666 557.5336)">
	<stop offset="0" style="stop-color:#D63305"/>
	<stop offset="0.366" style="stop-color:#CF3004"/>
	<stop offset="0.899" style="stop-color:#BC2602"/>
	<stop offset="1" style="stop-color:#B72401"/>
</linearGradient>
<path style="fill:url(#SVGID_6_);"
      d="M469.671,142.965L369.035,42.33l31.523-31.523c14.409-14.409,37.769-14.409,52.177,0  l48.459,48.459c14.409,14.409,14.409,37.769,0,52.177L469.671,142.965z"/>
<linearGradient id="SVGID_7_" gradientUnits="userSpaceOnUse" x1="462.6305" y1="417.3002" x2="444.2605" y2="435.6602"
                gradientTransform="matrix(1.0667 0 0 -1.0667 3.2666 557.5336)">
	<stop offset="0" style="stop-color:#960000"/>
	<stop offset="0.331" style="stop-color:#9C0700;stop-opacity:0.669"/>
	<stop offset="0.812" style="stop-color:#AE1A01;stop-opacity:0.188"/>
	<stop offset="1" style="stop-color:#B72401;stop-opacity:0"/>
</linearGradient>
<path style="fill:url(#SVGID_7_);"
      d="M436.309,109.603l33.362,33.362l31.524-31.524c14.407-14.407,14.407-37.767,0-52.176  l-7.275-7.275L436.309,109.603z"/>
<linearGradient id="SVGID_8_" gradientUnits="userSpaceOnUse" x1="393.8599" y1="439.5956" x2="381.0999" y2="426.8456"
                gradientTransform="matrix(1.0667 0 0 -1.0667 3.2666 557.5336)">
	<stop offset="0" style="stop-color:#FFFFFF"/>
	<stop offset="1" style="stop-color:#E8EFEE"/>
</linearGradient>
<polygon style="fill:url(#SVGID_8_);" points="474.17,138.466 373.534,37.831 334.621,76.744 435.257,177.379 "/>
<linearGradient id="SVGID_9_" gradientUnits="userSpaceOnUse" x1="367.5279" y1="413.2776" x2="359.2179" y2="404.9676"
                gradientTransform="matrix(1.0667 0 0 -1.0667 3.2666 557.5336)">
	<stop offset="0" style="stop-color:#FFFFFF"/>
	<stop offset="1" style="stop-color:#E8EFEE"/>
</linearGradient>
<polygon style="fill:url(#SVGID_9_);" points="448.228,164.409 347.592,63.773 334.621,76.744 435.257,177.379 "/>
<linearGradient id="SVGID_10_" gradientUnits="userSpaceOnUse" x1="339.2676" y1="385.0179" x2="360.7477" y2="406.4979"
                gradientTransform="matrix(1.0667 0 0 -1.0667 3.2666 557.5336)">
	<stop offset="0" style="stop-color:#FFC200;stop-opacity:0"/>
	<stop offset="0.203" style="stop-color:#FFBB00;stop-opacity:0.203"/>
	<stop offset="0.499" style="stop-color:#FFA700;stop-opacity:0.499"/>
	<stop offset="0.852" style="stop-color:#FF8800;stop-opacity:0.852"/>
	<stop offset="1" style="stop-color:#FF7800"/>
</linearGradient>
<polygon style="fill:url(#SVGID_10_);" points="418.631,194.004 317.995,93.369 334.621,76.744 435.257,177.379 "/>
<linearGradient id="SVGID_11_" gradientUnits="userSpaceOnUse" x1="381.2955" y1="427.05" x2="370.3555" y2="416.1"
                gradientTransform="matrix(1.0667 0 0 -1.0667 3.2666 557.5336)">
	<stop offset="0" style="stop-color:#FFFFFF"/>
	<stop offset="1" style="stop-color:#E8EFEE"/>
</linearGradient>
<polygon style="fill:url(#SVGID_11_);" points="461.199,151.437 360.563,50.801 347.592,63.773 448.228,164.409 "/>
<linearGradient id="SVGID_12_" gradientUnits="userSpaceOnUse" x1="19.9226" y1="65.6719" x2="-0.1164" y2="45.6419"
                gradientTransform="matrix(1.0667 0 0 -1.0667 3.2666 557.5336)">
	<stop offset="0" style="stop-color:#363F3E"/>
	<stop offset="1" style="stop-color:#303033"/>
</linearGradient>
<path style="fill:url(#SVGID_12_);"
      d="M10.981,471.179L0.339,503.464c-1.669,5.062,3.137,9.869,8.199,8.199l32.285-10.642  L10.981,471.179z"/>
<linearGradient id="SVGID_13_" gradientUnits="userSpaceOnUse" x1="403.9841" y1="393.8839" x2="428.6541" y2="369.2039"
                gradientTransform="matrix(1.0667 0 0 -1.0667 3.2666 557.5336)">
	<stop offset="0" style="stop-color:#C2CECE;stop-opacity:0"/>
	<stop offset="0.179" style="stop-color:#AFBCBC;stop-opacity:0.179"/>
	<stop offset="1" style="stop-color:#5B6A6A"/>
</linearGradient>
<polygon style="fill:url(#SVGID_13_);" points="474.17,138.466 440.808,105.104 401.895,144.017 435.257,177.379 "/>
<linearGradient id="SVGID_14_" gradientUnits="userSpaceOnUse" x1="346.5584" y1="451.3081" x2="371.2284" y2="426.6381"
                gradientTransform="matrix(1.0667 0 0 -1.0667 3.2666 557.5336)">
	<stop offset="0" style="stop-color:#C2CECE;stop-opacity:0"/>
	<stop offset="0.55" style="stop-color:#C2CECE"/>
	<stop offset="1" style="stop-color:#C2CECE;stop-opacity:0"/>
</linearGradient>
<polygon style="fill:url(#SVGID_14_);" points="423.15,87.447 389.788,54.084 350.875,92.997 384.237,126.36 "/>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
<g>
</g>
</svg>
          </span>
            <span>Редактировать личный объем</span>
          </div>
        </div>
      </div>
      <div class="tooltip-remove__edit"
           v-if="editing"
      >
        <input
          class="tooltip-remove__edit-input"
          type="text"
          v-number-filter
          v-autofocus
          v-model="selfVolume"
          placeholder="Введите значение"
          @keypress.enter="savePersonalVolume"
          maxlength="5"
        >
        <div class="tooltip-remove__edit__btn-group">
          <button @click="editing = false"
                  class="edit__btn edit__btn-cancel"
          >Cancel
          </button>
          <button
            @click="savePersonalVolume"
            class="edit__btn edit__btn-save"
          >Save
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import {mapActions, mapGetters} from 'vuex';
  import ClickOutside from 'vue-click-outside';

  export default {
    directives: {
      ClickOutside,
      numberFilter: {
        bind(el) {
          el.value = parseInt(el.value, 10);
        },
        inserted(el) {
          if (!el.value) el.value = 0
          let withoutChar = function (e) {
            el.value = e.target.value.replace(/[^\d]/, '')
            el.value = +el.value
          }
          el.addEventListener('input', withoutChar)
        },

      }
    },
    props: {
      card: Object,
    },
    data() {
      return {
        removeCard: 'children-tree',
        open: true,
        tooltipDeleted: false,
        editing: false,
        selfVolume: 0
      }
    },
    mounted() {
      this.selfVolume = this.card.l_amount || 0;
      document.body.addEventListener('keydown', this.closeByKeypress)
    },
    updated() {
      console.log(this.TOOLTIP_IS_OPEN)
    },
    computed: {
      ...mapGetters(['tooltip_is_show', 'TOOLTIP_IS_OPEN']),
      selfVolumeParsed() {
        return this.selfVolume ? parseInt(this.selfVolume, 10) : 0;
      }
    },
    methods: {
      ...mapActions(['closeTooltipCache']),
      focusOut(e) {
        if (e.currentTarget.contains(e.target) && !e.target.classList.contains('user-card__btn')) {
          this.savePersonalVolume();
          this.closeTooltipCache()
          return false;
        }
      },
      savePersonalVolume() {
        if (this.card.root && this.selfVolumeParsed <= 70) {
          return this.card.l_amount = 70;
        }
        this.card.l_amount = this.selfVolumeParsed;
        this.editing = false;
        this.closeTooltip();
      },
      closeTooltip() {
        this.tooltipDeleted = true;
        this.closeTooltipCache();
      },
      closeByKeypress(e) {
        if (this.card.tooltip.isOpen && e.key === 'Escape') {
          this.closeTooltip();
        }
      },
      deleteChildren() {
        this.card.list = this.card.list.slice(0, 0);
        this.closeTooltip();
      },
      deleteCardWithChildren() {
        let parent = this.card.parentCard;
        let parentChildren = parent.list;
        let elemIndex = parentChildren.indexOf(this.card);


        new Promise(resolve => {
          this.closeTooltip()
          resolve();
        }).then(() => {
          parentChildren.splice(elemIndex, 1)
        })
      },
      editPersonalVolume() {
        this.editing = true;
      }
    },
    beforeDestroy() {
      document.body.removeEventListener('keydown', this.closeByKeypress)
    }
  }
</script>

<style lang="scss">
  .tooltip-remove {
    width: auto;
    min-width: 100%;
    transform-origin: 0 50%;
    padding-bottom: 10px;

    &:focus {
      outline: none;

      .tooltip-remove__header {
        background: #324354;
        color: #fff;
      }

      .tooltip-remove__close {
        &:after,
        &:before {
          background: #fff;
        }
      }
    }

    &__close {
      position: absolute;
      z-index: 10;
      top: 2px;
      right: 2px;
      display: flex;
      justify-content: center;
      align-items: center;
      width: 20px;
      height: 20px;
      padding: 2px;
      outline: none;
      border-radius: 50%;
      transition: .3s;

      &:hover {
        background: rgba(#fff, .22);
      }

      &:before,
      &:after {
        content: '';
        position: absolute;
        display: block;
        width: 10px;
        height: 2px;
        background: rgba(#000, .4);
        top: 50%;
        left: 50%;
        transition: inherit;
      }

      &:before {
        transform: translate(-50%, -50%) rotate(45deg)
      }

      &:after {
        transform: translate(-50%, -50%) rotate(-45deg)
      }

      svg {
        pointer-events: none;
      }
    }

    &__header {
      font-size: 14px;
      font-weight: 600;
      background: #ffc107;
      color: #000;
      padding: 4px 10px;
      transition: .3s;
      display: flex;
      justify-content: center;
    }

    &__label {
      display: flex;
      align-items: center;
      padding: 8px 12px;
      white-space: nowrap;
      cursor: pointer;
      transition: .3s ease;
      font-size: 12px;
      color: #324354;

      &:hover {
        /*background: rgba(#ccc, .22);*/
        background: rgba(#ffc107, .33);
      }
    }

    &__edit {
      padding: 10px 10px 0;

      &-input {
        padding: 5px;
        margin-bottom: 15px;
        border: 1px solid #ccc;
        box-shadow: inset 0 1px 3px #ddd;
        border-radius: 4px;

        &:focus {
          box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075), 0 0 8px rgba(102, 175, 233, .6);
        }

      }

      &__btn-group {
        display: flex;
        justify-content: space-between;
      }
    }

    &__icon {
      display: flex;
      width: 18px;
      margin-right: 10px;
    }
  }

  .edit__btn {
    width: 45%;
    padding: 5px;
    font-size: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 2px;
    transition: .3s ease;
    border: 1px solid transparent;

    &-cancel {
      background: transparent;
      border-color: rgba(#363F3E, .4);

      &:hover {
        background: rgba(#363F3E, 1);
        color: #ffc107;
      }

      /*box-shadow: inset 0 0 1px 1px rgba(0, 0, 0, .5);*/
    }

    &-save {
      background: #ffc107;

      &:hover {
        background: darken(#ffc107, 5%);
      }
    }
  }
</style>