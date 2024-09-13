<template>
  <svg
    fill="none"
    viewBox="0 0 24 24"
    xmlns="http://www.w3.org/2000/svg"
    class="icon-filter"
  >
    <g fill="black">
      <path
        d="m10.0833 15.958h-6.57553c-.83222 0-1.50777.6637-1.50777 1.4813 0 .8165.67555 1.4813 1.50777 1.4813h6.57553c.8322 0 1.5078-.6648 1.5078-1.4813 0-.8176-.6756-1.4813-1.5078-1.4813z"
        opacity=".4"
        class="line-bottom"
      />
      <path
        d="m22 6.37856c0-.81653-.6756-1.48024-1.5067-1.48024h-6.5755c-.8322 0-1.5078.66371-1.5078 1.48024 0 .81762.6756 1.48133 1.5078 1.48133h6.5755c.8311 0 1.5067-.66371 1.5067-1.48133z"
        opacity=".4"
        class="line-top"
      />
      <path
        d="m8.87774 6.37856c0 1.86667-1.53888 3.37965-3.43887 3.37965-1.89888 0-3.43887-1.51298-3.43887-3.37965 0-1.86558 1.53999-3.37856 3.43887-3.37856 1.89999 0 3.43887 1.51298 3.43887 3.37856z"
        class="circle-top"
      />
      <path
        d="m22.0001 17.3992c0 1.8656-1.5389 3.3786-3.4389 3.3786-1.8989 0-3.4389-1.513-3.4389-3.3786 0-1.8667 1.54-3.3796 3.4389-3.3796 1.9 0 3.4389 1.5129 3.4389 3.3796z"
        class="circle-bottom"
      />
    </g>
  </svg>
</template>

<style scoped>
.icon-filter {
  cursor: pointer;
}

.icon-filter .line-bottom,
.icon-filter .line-top {
  transition: all 0.2s ease;
}

.icon-filter .circle-bottom,
.icon-filter .circle-top {
  transition: all 0.3s ease;
}

.icon-filter:hover .line-bottom {
  transform: translateX(10px);
}
.icon-filter:hover .line-top {
  transform: translateX(-10px);
}
.icon-filter:hover .circle-bottom {
  transform: translateX(-13px);
}
.icon-filter:hover .circle-top {
  transform: translateX(13px);
}
</style>
