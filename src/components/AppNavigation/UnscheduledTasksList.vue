<!--
  - SPDX-FileCopyrightText: 2021 Nextcloud GmbH and Nextcloud contributors
  - SPDX-License-Identifier: AGPL-3.0-or-later
-->

<template>
	<!--
	 The appointments feature requires at least one calendar in the vuex store.
	 Trying to use it before calendars are loaded will result in an error.
	-->
	<div v-if="hasAtLeastOneCalendar && tasks.length > 0"
		class="unscheduled-tasks-list">
		<AppNavigationCaption class="unscheduled-tasks-list__caption"
			:name="t('calendar', 'Unscheduled Tasks')">
		</AppNavigationCaption>

		<template>
			<template v-if="tasks.length > 0">
				<UnscheduledTasksListItem v-for="config in tasks"
					:key="config.id"
					:config="config"
					:color="(calendarsStore.getCalendarById(config.extendedProps.calendarId)).color"/>
			</template>
		</template>
	</div>
</template>

<script>
import UnscheduledTasksListItem from './UnscheduledTasksList/UnscheduledTasksListItem.vue'
import {
	NcAppNavigationCaption as AppNavigationCaption,
} from '@nextcloud/vue'
import { translate as t, translatePlural as n} from '@nextcloud/l10n'
import useCalendarsStore from '../../store/calendars.js'
import useTasksStore from '../../store/unscheduledtasks.js'
import { mapStores } from 'pinia'

export default {
	name: 'UnscheduledTasksList',
	components: {
		UnscheduledTasksListItem,
		AppNavigationCaption,
	},

	computed: {
		...mapStores(useCalendarsStore, useTasksStore),

		tasks() {
			return this.tasksStore.GetTasks
		},

		hasAtLeastOneCalendar() {
			return !!this.calendarsStore.ownSortedCalendars[0]
		},
	},
}
</script>
