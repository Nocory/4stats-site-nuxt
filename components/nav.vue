<template>
  <div class="component-nav">
		
    <div class="title-and-description">
      <router-link to="/">
        <div class="site-title">4stats.io</div>
      </router-link>
      <div class="site-description is-hidden-mobile">Currently {{ combinedBoardStats.postsPerMinute.toFixed(2) }} posts/minute with ~{{ Math.round(combinedBoardStats.avgPostsPerDay / 1000) }}k posts/day</div>
    </div>

    <no-ssr>
      <router-link :to="this.$route.path != '/config' ? '/config' : '/'">
        <button class="config-button" @click="showConfig = true">
          <template v-if="this.$route.path != '/config'">
            <span class="icon">
              <i class="fa-lg fa-cog"/>
            </span>
            <span class="config-button-text">
              Boards
            </span>
          </template>
          <template v-else>
            <span class="config-button-text">
              Save ✔
            </span>
          </template>
        </button>
      </router-link>
    </no-ssr>
			
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
export default {
	data: () => ({
		//url: location.hostname,
		url: "4stats.io"
	}),
	computed: {
		...mapGetters(['combinedBoardStats'])
	}
}
</script>

<style scoped lang="scss">
@import "~assets/css/variables.scss";

.component-nav{
	z-index: 10;
	position: relative;
	background: $--color-navbar;
	color: $--color-text;
	@include tablet{
		box-shadow: 0px 0px 12px 0px rgba(0,0,0,0.5);
	}
	padding: 0 1rem;
	position: relative;
	display: flex;
	align-items: center;
}

a:active, a:focus, button:active, button:focus {
  outline: 0;
  border: none;
}

.title-and-description{
	display: flex;
	justify-content: flex-start;
	align-items: baseline;
	flex-grow: 1;
}

.site-title{
	color: $--color-text;
	position: relative;
	line-height: 1.5;
	@include touch{
		margin-left: 1rem;
	}
	font-size: 2rem;
}

.site-description{
	padding: 0 1rem;
}

.config-button{
	position: relative;
	@include touch{
		margin-right: 1rem;
	}
	display: flex;
	align-items: center;
	cursor: pointer;
	padding: 0;
	border: none;
	background: transparent;
	color: $--color-text;
	font-weight: bolder;

	//underline
	&::before{
		z-index: 0;
		content:"";
		position: absolute;
		background: $--color-link;
		top: 100%;
		right: 0;
		height: 2px;
		width: 100%;
		transform: skew(-45deg);
	}

	>.icon{
		z-index: 1;
	}

	>.config-button-text{
		font-size: 1.25rem;
		z-index: 1;
		font-family: monospace;
		padding: 0 0 0 0.25rem;
	}
}


</style>