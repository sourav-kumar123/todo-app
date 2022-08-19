<template>
	<div>

		<v-container>
			<v-row justify="space-between">
				<v-col
					cols="12"
					md="4"
				>
					<v-form v-on:submit.prevent>
						<v-text-field
							v-model="name"
							type="text"
							label="Name"
							required
						></v-text-field>

						<v-btn
							v-on:click="submit()"
							color="success"
							class="mr-4"
							@keyup.13="submit()"
						>
							submit
						</v-btn>

					</v-form>
				</v-col>
			</v-row>
		</v-container>

		<v-container>
			<v-row justify="space-between">
				<v-col
					cols="12"
					md="4"
				>

					<v-list-item
						v-for="(item, index) in list"
						:key="index"
						:value="item"
					>

						<v-list-item-content style="border:2px solid black">
							<v-row>
								<v-col
									cols="3"
									:class="{ hide:item.iscompleted  }"
								>

									{{ item.name }} ,{{item.timestamp }}
								</v-col>

								<v-col cols="3">
									<v-btn
										@click="completed(index)"
										color="success"
										class="mr-4"
									>
										Completed
									</v-btn>
								</v-col>
								<v-col cols="3">
									<v-btn
										v-on:click="Edit(item, index)"
										color="success"
										class="mr-1"
										:disabled="item.iscompleted == true"
									>
										Edit
									</v-btn>
								</v-col>
								<v-col cols="3">
									<v-btn
										v-on:click="close(index)"
										color="success"
										class="mr-4"
									>
										Delete
									</v-btn>
								</v-col>
							</v-row>
						</v-list-item-content>
					</v-list-item>

				</v-col>
			</v-row>
		</v-container>
	</div>
</template>

<script>
	export default {
		name: "HelloWorld",
		data() {
			return {
				hidden: false,
				name: "",
				list: [],
				isEdit: null,
				disabled: "",
				arr: [],
			};
		},
		methods: {
			submit( ) {
				const today = new Date();
				this.monthNames = [
					"January",
					"February",
					"March",
					"April",
					"May",
					"June",
					"July",
					"August",
					"September",
					"October",
					"November",
					"December",
				];
				this.timestamp =
					today.getDate() +
					" " +
					this.monthNames[today.getMonth()] +
					"," +
					today.getHours() +
					":" +
					today.getMinutes() +
					":" +
					today.getSeconds();

				if (this.name.trim()) {
					let obj = {
						name: this.name,
						iscompleted: this.iscompleted,
						timestamp: this.timestamp,
					};

					
						this.list.push(obj);
					
					this.name = "";
					this.isEdit = null;
					this.timestamp = "";
					this.iscompleted=false;
				}
				
			},
			close(index) {
				{
					this.list.splice(index, 1);
				}
				this.name = "";
			},
			Edit(item, index) {
				this.isEdit = index;
				this.name = item.name;
				
				
			},
			completed( index) {
				this.list[index].iscompleted=true;
								
			},
		},
	};
</script>
<style scoped>
.hide {
	text-decoration-line: line-through;
}
</style>
