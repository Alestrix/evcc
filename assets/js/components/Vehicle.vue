<template>
	<div>
		<div class="mb-3">
			{{ vehicleTitle || $t("main.vehicle.fallbackName") }}
		</div>
		<VehicleSoc v-bind="vehicleSocProps" @target-soc-updated="targetSocUpdated" />
		<VehicleSubline
			v-bind="vehicleSubline"
			@target-time-updated="targetTimeUpdated"
			class="my-1"
		/>
	</div>
</template>

<script>
import collector from "../mixins/collector";

import VehicleSoc from "./VehicleSoc";
import VehicleSubline from "./VehicleSubline";

export default {
	name: "Vehicle",
	components: { VehicleSoc, VehicleSubline },
	props: {
		id: Number,
		connected: Boolean,
		vehiclePresent: Boolean,
		vehicleSoc: Number,
		enabled: Boolean,
		charging: Boolean,
		minSoC: Number,
		vehicleTitle: String,
		timerActive: Boolean,
		timerSet: Boolean,
		targetTime: String,
		targetSoC: Number,
	},
	computed: {
		vehicleSocProps: function () {
			return this.collectProps(VehicleSoc);
		},
		vehicleSubline: function () {
			return this.collectProps(VehicleSubline);
		},
	},
	methods: {
		targetSocUpdated: function (targetSoC) {
			this.$emit("target-soc-updated", targetSoC);
		},
		targetTimeUpdated: function (targetTime) {
			this.$emit("target-time-updated", targetTime);
		},
	},
	mixins: [collector],
};
</script>
