<script lang="ts">
  type ListItemType = {
    id: number;
    title: string;
    checked: boolean;
  };
  let text: string = "";
  let list: Array<ListItemType> = [];

  const onClickCheckBox = (id: number) => {
    const fIdx = list.findIndex((v) => v.id === id);
    if (fIdx !== -1) {
      list[fIdx].checked = !list[fIdx].checked;
    }
  };

  const onClickAdd = () => {
    if (text !== "") {
      const newList: ListItemType = {
        id: Math.floor(Math.random() * 100),
        title: text,
        checked: false,
      };
      list = [...list, newList];
      text = "";
    }
  };

  const onClickDelete = (id: number) => {
    list = list.filter((v) => v.id !== id);
  };

  const onPressEnter = (e: KeyboardEvent) => {
    if (e.keyCode === 13) {
      onClickAdd();
    }
  };
</script>

<div class="todo-list-container">
  <div class="input-container">
    <div class="input">
      <input bind:value={text} type="text" />
    </div>
    <div class="btn-container">
      <div on:mousedown={(e) => onClickAdd()} class="btn-add">+ Add TODO</div>
    </div>
  </div>
  {#each list as listItem, i}
    <div class="list-item">
      <div
        on:mousedown={(e) => onClickCheckBox(listItem.id)}
        class={`check ${listItem.checked && "checked"}`}
      >
        <div class="checkbox" />
      </div>
      <div class={`title ${listItem.checked && "checked"}`}>
        {listItem.title}
      </div>
      <div class="btn-group">
        <div class="edit list-btn">수정</div>
        <div
          on:mousedown={(e) => onClickDelete(listItem.id)}
          class="delete list-btn"
        >
          삭제
        </div>
      </div>
    </div>
  {/each}
</div>

<svelte:window on:keydown={onPressEnter} />

<style lang="scss">
  .todo-list-container {
    width: 60%;
    display: flex;
    flex-direction: column;
    gap: 8px;
    align-items: center;

    .input-container {
      display: flex;
      align-items: center;
      width: 100%;
      .input {
        width: 90%;
        height: 32px;
        input {
          height: 100%;
          width: 90%;
        }
      }

      .btn-container {
        margin-left: auto;
        width: 120px;
        border: 1px solid black;
        cursor: pointer;
        text-align: center;
        padding: 16px 24px;
      }
      margin-bottom: 16px;
    }

    .list-item {
      padding: 8px;
      display: flex;
      width: 100%;
      border: 1px solid black;
      align-items: center;
      .check {
        margin-right: 16px;
        .checkbox {
          width: 16px;
          height: 16px;
          border: 1px solid black;
          cursor: pointer;
        }
        &.checked {
          .checkbox {
            background-color: black;
          }
        }
      }
      .title {
        &.checked {
          color: gray;
          text-decoration: line-through;
        }
      }
      .btn-group {
        display: flex;
        gap: 6px;
        margin-left: auto;
        .list-btn {
          border: 1px solid black;
          padding: 8px;
        }
        .edit {
          cursor: not-allowed;
        }
        .delete {
          cursor: pointer;
        }
      }
    }
  }
</style>
