<script>
	export default {
		beforeCreate() {
			
		},
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	html,
	body,
	div,
	form,
	p,
	ul,
	li,
	h1,
	h2,
	h3,
	h4,
	h5,
	h6,
	img,
	input,
	textarea,
	table,
	tr,
	td,
	ol,
	dl,
	dd,
	dt {
		margin: 0;
		padding: 0;
	}

	ul,
	ol,
	dl {
		list-style: none;
	}

	a {
		text-decoration: none;
		border: none;
	}

	input,
	textarea,
	button {
		outline: none;
	}
	.status_bar {
			height: var(--status-bar-height)!important;
			width: 100%!important;
			background-color: #f1f5f9!important;
			color:#fff!important;
		}

		.top_view {
			height: var(--status-bar-height)!important;
			width: 100%!important;
			position: fixed!important;
			background-color: #f1f5f9!important;
			top: 0!important;
			z-index: 99999!important;
		}
</style>