<template>
<div class="mmnnbwxb">
	<portal to="icon"><fa :icon="faInfoCircle"/></portal>
	<portal to="title">{{ $t('about') }}</portal>

	<section class="_section info" v-if="meta">
		<div class="_title"><fa :icon="faInfoCircle"/> {{ $t('instanceInfo') }}</div>
		<div class="_content" v-if="meta.description">
			<div>{{ meta.description }}</div>
		</div>
		<div class="_content table">
			<div><b>{{ $t('administrator') }}</b><span>{{ meta.maintainerName }}</span></div>
			<div><b></b><span>{{ meta.maintainerEmail }}</span></div>
		</div>
		<div class="_content table" v-if="stats">
			<div><b>{{ $t('users') }}</b><span>{{ stats.originalUsersCount | number }}</span></div>
			<div><b>{{ $t('notes') }}</b><span>{{ stats.originalNotesCount | number }}</span></div>
		</div>
		<div class="_content table">
			<div><b>Misskey</b><span>v{{ version }}</span></div>
		</div>
	</section>

	<section class="_section aboutMisskey">
		<div class="_title"><fa :icon="faInfoCircle"/> {{ $t('aboutMisskey') }}</div>
		<div class="_content">
			<div style="margin-bottom: 1em;">{{ $t('aboutMisskeyText') }}</div>
			<div>{{ $t('misskeyMembers') }}</div>
			<span class="members">
				<a href="https://github.com/syuilo" target="_blank">@syuilo</a>
				<a href="https://github.com/AyaMorisawa" target="_blank">@AyaMorisawa</a>
				<a href="https://github.com/mei23" target="_blank">@mei23</a>
				<a href="https://github.com/acid-chicken" target="_blank">@acid-chicken</a>
				<a href="https://github.com/tamaina" target="_blank">@tamaina</a>
				<a href="https://github.com/rinsuki" target="_blank">@rinsuki</a>
			</span>
			<div style="margin-top: 1em;">{{ $t('misskeySource') }}</div>
			<a href="https://github.com/syuilo/misskey" target="_blank" style="color: var(--link);">https://github.com/syuilo/misskey</a>
		</div>
	</section>
</div>
</template>

<script lang="ts">
import Vue from 'vue';
import { faInfoCircle } from '@fortawesome/free-solid-svg-icons';
import { version } from '../config';
import i18n from '../i18n';

export default Vue.extend({
	i18n,

	metaInfo() {
		return {
			title: this.$t('instance') as string
		};
	},

	data() {
		return {
			version,
			meta: null,
			stats: null,
			serverInfo: null,
			faInfoCircle
		}
	},

	created() {
		this.$root.getMeta().then(meta => {
			this.meta = meta;
		});

		this.$root.api('stats').then(res => {
			this.stats = res;
		});
	},
});
</script>

<style lang="scss" scoped>
.mmnnbwxb {
	> .info {
		> .table {
			> div {
				display: flex;

				> * {
					flex: 1;
				}
			}
		}
	}

	> .aboutMisskey {
		> ._content {
			> .members {
				> a {
					color: var(--link);
					margin-right: 0.5em;
				}
			}
		}
	}
}
</style>
