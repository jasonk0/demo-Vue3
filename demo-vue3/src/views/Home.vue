<template>
	<div class="container">
		<h1>TodoList</h1>
		<h3>
			已列入事项<span class="text-primary">{{ lists.length }}</span
			>，已完成事项<span class="text-success">{{ finished.length }}</span>
		</h3>
		<h3>未完成的列表</h3>
		<ul class="list-group">
			<li
				class="list-group-item"
				v-for="(item, index) in lists"
				:key="index"
				@click="item.checked = !item.checked"
				v-show="!item.checked"
			>
				<div class="form-check">
					<input
						class="form-check-input"
						type="checkbox"
						value=""
						:id="'item-' + index"
						v-model="item.checked"
					/>
					<label class="form-check-label" :for="'item-' + index">
						{{ item.name }}
					</label>
				</div>
			</li>
		</ul>
		<h3>已完成的列表</h3>
		<ul class="list-group">
			<li
				class="list-group-item"
				v-for="(item, index) in finished"
				:key="'finished-' + index"
			>
				<div class="form-check">
					<input
						class="form-check-input"
						type="checkbox"
						value=""
						:id="'finished-' + index"
						disabled
					/>
					<label class="form-check-label" :for="'finished-' + index">
						{{ item.name }}
					</label>
				</div>
			</li>
		</ul>
		<h3>添加新的Tasks</h3>
		<div class="form-floating mb-3">
			<input
				type="text"
				class="form-control"
				id="floatingInput"
				placeholder="listEvent"
				v-model="value"
        @keydown.enter="addList"
			/>
			<label for="floatingInput">新的事项...</label>
		</div>
		<div class="d-grid gap-2">
			<button class="btn btn-primary" type="button" @click="addList">
				确定添加
			</button>
		</div>
	</div>
</template>

<script >
import { toRefs, reactive, computed } from "vue";

export default {
	name: "Home",
  
	// 1.加入chexbox -> checked
	// 2.统计checked
	// 3.add添加item -> item数据结构
	// 4.双击进行编辑
	// 5.删除功能 -> 删除特定index的元素
  

	setup() {
    const addList = () => {
      state.lists.push({
        name: state.value,
        checked: false,
        isEdit: false,
      })
      state.value = ''
    }

		const state = reactive({
      value: '',
			lists: [
				{
					name: 1,
					checked: false,
					isEdit: false,
				},
				{
					name: 2,
					checked: false,
					isEdit: false,
				},
				{
					name: 3,
					checked: false,
					isEdit: false,
				},
			],
      addList,
			// finished1: computed(() => state.list = 'demo' + 1),
			finished: computed(() =>
				state.lists.filter((item) => item.checked == true)
			),
		});

		return toRefs(state);
	},
};
</script>
