
  - SPDX-FileCopyrightText: 2021 Nextcloud GmbH and Nextcloud contributors
  - SPDX-License-Identifier: AGPL-3.0-or-later
-->

<template>
  <div :id="config.id + '-1'" :data-event="JSON.stringify({ title: config.title })" style="margin-bottom: 12px; ; margin-left: 6px;">
    <div
      class="fc-event fc-h-event fc-daygrid-event fc-daygrid-block-event"
      style="background-color: transparent !important; border: none !important; box-shadow: none !important;"
    >
      <div
        class="event-content"
        style="display: flex; align-items: center; gap: 8px;"
      >
        <div
          class="icon-wrapper"
          :style="{ backgroundColor: color, minWidth: '10px', minHeight: '10px', width: '10px', height: '10px',  display: 'inline-flex', alignItems: 'center', justifyContent: 'center', borderRadius: '50%', flexShrink: 0 }"
        >
        </div>
        <span
          class="event-title"
          style="white-space: nowrap; overflow: hidden; text-overflow: ellipsis; font-size: 14px; font-weight: 500; display: block;"
        >
          {{ config.title }}
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import { showError, showSuccess } from '@nextcloud/dialogs'
import logger from '../../../utils/logger.js'
import { Draggable } from '@fullcalendar/interaction'

export default {
	name: 'UnscheduledTasksListItem',

	mounted() {
		var containerEl = document.getElementById(this.config.id + '-1');
		new Draggable(containerEl, {
			itemSelector: '.fc-event',
			eventData: this.config,
		})
	},
	props: {
		config: {
			type: Object,
			required: true,
		},
		color: {
			type: String,
			required: false, // or true if needed
			default: '#000000', // optional default value
		},
	},
}
</script>